# IDOR - Santa’s Little IDOR
  > Learn about IDOR while helping pentest the TrypresentMe website.

## Task 1 -> Introduction:
  > The elves of Wareville are on high alert since McSkidy went missing. Recently, the support team has been receiving many calls from parents who can't activate vouchers on the TryPresentMe website. They also mentioned they are receiving many targeted phishing emails containing information that is not public. The support team is wary and has enlisted the help of the TBFC staff. When looking into this peculiar case, they discovered a suspiciously named account named Sir Carrotbane, which has many vouchers assigned to it. For now, they have deleted the account and retrieved the vouchers. But something is going on. Can you help the TBFC staff investigate the TryPresentMe website and fix the vulnerabilities?

- ``` My target machine and the AttackBox have started and I am ready to learn about IDOR. ``` marks the completion of Task 1.

## Task 2 -> IDOR on the Shelf
  ### It’s Dangerously Obvious, Really
  > Have you ever seen a link that looks like this: https://awesome.website.thm/TrackPackage?packageID=1001?
    When you saw a link like this, have you ever wondered what would happen if you simply changed the packageID to 11 or 12? In its simplest form, this can be a potential case for IDOR. 
IDOR stands for Insecure Direct Object Reference and is a type of access control vulnerability. Web applications often use references to determine what data to return when you make a request. However, if the web server doesn't perform checks to ensure you are allowed to view that data before sending it, it can lead to serious sensitive information disclosure. A good question to ask then is:
Why does this happen so often?

> If the user wants to know the status of their package and makes a web request, the simplest method is to allow the user to supply their packageID. We recover data from the database using the simplest SQL query of:

``` SELECT person, address, status FROM Packages WHERE packageID = value; ``` 

> However, since packageID is a sequential number, it becomes pretty obvious to guess the packageIDs of other customers, and since the web application isn't verifying that the person making the request is the same person as the one who owns the package, an IDOR vulnerability appears, allowing attackers to recover the details for packages belonging to other users. Even worse is when a feature like this doesn't require a user to authenticate, then there would be no way to even tell who is making the request! To dive a bit deeper, we need to understand authentication, authorization, and privilege escalation.

### Identity Defines Our Reach
> To understand the root cause of IDOR, it is important to understand the basic principles of authentication and authorization:

>Authentication: The process by which you verify who you are. For example, supplying your username and password.

>Authorization: The process by which the web application verifies your permissions. For example, are you allowed to visit the admin page of a web application, or are you allowed to make a payment using a specific account?

>You may think that authentication only happens once when you supply your username and password, but that is actually not the case! After providing your credentials, you receive a cookie or a token, called session information. Every subsequent request you make to the application includes this session information, which is verified by the application. This initial verification process is still authentication and happens for each request. This is why websites will often redirect you back to the login page. It means your session information has expired, and thus, you need to reauthenticate with your credentials to receive new session information.

## Answers:
### What does IDOR stand for?
  > Insecure Direct Object Reference
### What type of privilege escalation are most IDOR cases?
  > Horizontal
### Exploiting the IDOR found in the view_accounts parameter, what is the user_id of the parent that has 10 children?
  > 15

## Concepts Learned:
- Learned about IDOR
- Got to know about how to seek into different user's data by changing their user_id.

## Solution:
- Login into the website using the given credentials.
- Opened ``` Developer's Tool ```.
- Opened Network and refresh the page.
- All the requests in the web server were displayed.
- Opened ``` viewaccountinfo ``` request and analyzed the reponse.

  <img width="1440" height="303" alt="image" src="https://github.com/user-attachments/assets/2341d8e8-d076-47f9-8061-31c3348f7296" />

- Went to ``` Storage ``` tab and then to Local Storage.
- Changed ``` user_id ``` one by one until the user has 10 children.
- On the id which has 10 children, was the answer.


