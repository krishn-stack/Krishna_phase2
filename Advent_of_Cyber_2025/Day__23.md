# AWS Security - S3cret Santa
 > Learn the basics of AWS enumeration.

## Task 1 -> Introduction
 > One of our stealthiest infiltrated elves managed to hop their way into Sir Carrotbane’s office and, lo and behold, discovered a bundle of cloud credentials just lying around on his desktop like forgotten carrots. The agent suspects these could be the key to regaining access to TBFC’s cloud network. If only the poor hare had the faintest clue what “the cloud” is, he’d burrow in himself. Let's help the elf utilise these credentials to try to regain access to TBFC's cloud network.

AWS accounts can be accessed programmatically by using an Access Key ID and a Secret Access Key. For this room, both of those will be automatically configured for you. The AWS CLI will look for credentials at ``` ~/.aws/credentials ```

## Solution:
- Opened terminal, ``` ls -a ``` in the home directory got ```.aws```.
- Used ``` cat .aws/credentials ``` to get ``` aws_access_key_id ``` and ``` aws_secret_access_key ```
  > Amazon Security Token Service (STS) allows us to utilise the credentials of a user that we have saved during our AWS CLI configuration. We can use the get-caller-identity call to retrieve information about the user we have configured for the AWS CLI.
- Ran ``` aws sts get-caller-identity ``` and got the answer to the first question i.e. Account number.

  ## Answer:
  ***Run aws sts get-caller-identity. What is the number shown for the "Account" parameter?***
  ```
  123456789012
  ```

## Task 2 -> IAM: Users, Roles, Groups and Policies
 ### IAM Overview
  > Amazon Web Services utilises the Identity and Access Management (IAM) service to manage users and their access to various resources, including the actions that can be performed against those resources. Therefore, it is crucial to ensure that the correct access is assigned to each user according to the requirements. Misconfiguring IAM has led to several high-profile security incidents in the past, giving attackers access to resources they were not supposed to access. Companies like Toyota, Accenture and Verizon have been victims of such attacks in the past, often exposing customer data or sensitive documents. Below, we will discuss the different aspects of IAM that can lead to sensitive data exposure if misconfigured.

### IAM Users
 > A user represents a single identity in AWS. Each user has a set of credentials, such as passwords or access keys, that can be used to access resources. Furthermore, permissions can be granted at a user level, defining the level of access a user might have.

### IAM Groups
  > Multiple users can be combined into a group. This can be done to ease the access management for multiple users. For example, in an organisation employing hundreds of thousands of people, there might be a handful of people who need write access to a certain database. Instead of granting access to each user individually, the admin can grant access to a group and add all users who require write access to that group. When a user no longer needs access, they can be removed from the group.

### IAM Roles
 > An IAM Role is a temporary identity that can be assumed by a user, as well as by services or external accounts, to get certain permissions.

### IAM Policies
 > Access provided to any user, group or role is controlled through IAM policies. A policy is a JSON document that defines the following:

> 1. What action is allowed (Action)
> 2. On which resources (Resource)
> 3. Under which conditions (Condition)
> 4. For whom (Principal)

## Answer:
***What IAM component is used to describe the permissions to be assigned to a user or a group?***
```
policy
```

## Task 3 -> Practical: Enumerating a User's Permissions
### Enumerating Users
 > Alright, let's see what we can do with the credentials we got from Sir Carrotbane's office, since we have already configured them in our environment. We can start interacting with the AWS CLI to find more information.
### Enumerating User Policies
 > Policies can be inline or attached. ***Inline policies*** are assigned directly in the user (or group/role) profile and hence will be deleted if the identity is deleted. These can be considered as hard-coded policies as they are hard-coded in the identity definitions. ***Attached policies***, also called managed policies, can be considered reusable. An attached policy requires only one change in the policy, and every identity that policy is attached to will inherit that change automatically.

## Solution:
- Ran following commands:
  - ``` aws iam list-users ```
  - ``` aws iam list-user-policies --user-name sir.carrotbane ```
  - ``` aws iam list-attached-user-policies --user-name sir.carrotbane ```
  - ``` aws iam list-groups-for-user --user-name sir.carrotbane ```
  - ``` aws iam get-user-policy --policy-name POLICYNAME --user-name sir.carrotbane ```
- Got the policyname.

## Answer:
***What is the name of the policy assigned to ``` sir.carrotbane ```?***
```
SirCarrotbanePolicy
```

## Task 4 -> Assuming Roles
### Enumerating Roles
 > The sts:AssumeRole action we previously found allows sir.carrotbane to assume roles. Perhaps we can try to see if there's any interesting ones available.

## Solution:
- Ran ``` aws iam list-roles ```
- Got ``` bucketmaster ``` role which can be assumed by sir.carrotbane.
- Then ran following commands:
  - ``` aws iam list-role-policies --role-name bucketmaster ```
  - ``` aws iam list-attached-role-policies --role-name bucketmaster ```
  - ``` aws iam get-role-policy --role-name bucketmaster --policy-name BucketMasterPolicy ```
  - Got a Policy(JSON document)
    ```
    {
    "RoleName": "bucketmaster",
    "PolicyName": "BucketMasterPolicy",
    "PolicyDocument": {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Action": [
                    "s3:ListAllMyBuckets"
                ],
                "Effect": "Allow",
                "Resource": "*",
                "Sid": "ListAllBuckets"
            },
            {
                "Action": [
                    "s3:ListBucket"
                ],
                "Effect": "Allow",
                "Resource": [
                    "arn:aws:s3:::easter-secrets-123145",
                    "arn:aws:s3:::bunny-website-645341"
                ],
                "Sid": "ListBuckets"
            },
            {
                "Action": [
                    "s3:GetObject"
                ],
                "Effect": "Allow",
                "Resource": "arn:aws:s3:::easter-secrets-123145/*",
                "Sid": "GetObjectsFromEasterSecrets"
            }
        ]
    }
    }
    ```

- Ran ``` aws sts assume-role --role-arn arn:aws:iam::123456789012:role/bucketmaster --role-session-name TBFC ```
- Got this ``` AccessKeyId ```, ``` SecretAccessKey ```, ``` SessionToken ```
- Then ran following:
  - ``` export AWS_ACCESS_KEY_ID="ASIAxxxxxxxxxxxx" ```
  - ``` export AWS_SECRET_ACCESS_KEY="abcd1234xxxxxxxxxxxx" ```
  - ``` export AWS_SESSION_TOKEN="FwoGZXIvYXdzEJr..." ```

## Answer:
***Apart from GetObject and ListBucket, what other action can be taken by assuming the bucketmaster role?***
```
ListAllMyBuckets
```

## Task 5 -> Grabbing a file from S3
 ### What Is S3?
  > Amazon S3 stands for Simple Storage Service. It is an object storage service provided by Amazon Web Services that can store any type of object such as images, documents, logs and backup files. Companies often use S3 to store data for various reasons, such as reference images for their website, documents to be shared with clients, or files used by internal services for internal processing. Any object you store in S3 will be put into a "Bucket". You can think of a bucket as a directory where you can store files, but in the cloud.

## Solution:
- Ran following commands:
  - ``` aws s3api list-buckets ```
  - ``` aws s3api list-objects --bucket easter-secrets-123145 ```
  - ``` aws s3api get-object --bucket easter-secrets-123145 --key cloud_password.txt cloud_password.txt ```
- Ran ``` cat cloud_password.txt ``` and got the flag.

  ## Flag:
  ```
  THM{more_like_sir_cloudbane}
  ```
  
  
