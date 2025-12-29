# Authentication vulnerabilities
 > Authentication vulnerabilities can allow attackers to gain access to sensitive data and functionality. They also expose additional attack surface for further exploits.

## What is Authentication and Authorization ?
- ***Authentication:*** Authentication is the process of verifying that a user is who they claim to be.

  > It determines whether someone attempting to access a website with the username ``` Carlos123 ``` really is the same person who created the account.

- ***Authorization:*** Authorization involves verifying whether a user is allowed to do something.

  > Once ``` Carlos123 ``` is authenticated, their permissions determine what they are authorized to do.

## Brute-force attacks
A brute-force attack is when an attacker uses a system of trial and error to guess valid user credentials. These attacks are typically automated using wordlists of usernames and passwords.
 > Brute-forcing is not always just a case of making completely random guesses at usernames and passwords. By also using basic logic or publicly available knowledge, attackers can fine-tune brute-force attacks to make much more educated guesses.

### 1. Brute-forcing usernames
 > Usernames are especially easy to guess if they conform to a recognizable pattern, such as an email address.

***For example:***
```
firstname.lastname@somecompany.com
```
How to check for potential usernames:
- During auditing, check whether the website discloses potential usernames publicly.
- You should also check HTTP responses to see if any email addresses are disclosed.

### 2. Brute-forcing passwords
 > Passwords can similarly be brute-forced, with the difficulty varying based on the strength of the password.

Many websites adopt some form of password policy. This typically involves enforcing passwords with:
- A minimum number of characters
- A mixture of lower and uppercase letters
- At least one special character

While these websites adopt these password policy but we can exploit this by having:<br>
A basic knowledge of human behavior to exploit the vulnerabilities that users unwittingly introduce to this system. Rather than creating a strong password with a random combination of characters, users often take a password that they can remember and try to crowbar it into fitting the password policy. 
***For example:*** if ``` mypassword ``` is not allowed, users may try something like ``` Mypassword1! ``` or ``` Myp4$$w0rd ``` instead.

## Username enumeration
> Username enumeration is when an attacker is able to observe changes in the website's behavior in order to identify whether a given username is valid.

# Lab-1: Username enumeration via different responses
> This lab is vulnerable to username enumeration and password brute-force attacks. It has an account with a predictable username and password, which can be found in the following wordlists:<br>
> 1. [Candidate usernames](https://portswigger.net/web-security/authentication/auth-lab-usernames)<br>
> 2. [Candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords)<br>
> To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page.

## Solution:
- Accessed the lab and got this dashboard.

   <img width="1900" height="997" alt="image" src="https://github.com/user-attachments/assets/494b9563-9242-42ac-b2d6-6f5aad03cb1a" />

- Went to ``` My Account ``` and tried logging in one of the username and password from the given lists in the description:
   ***username*** -> ``` carlos ```
   ***password*** -> ``` password ```

- Opened BurpSuite and looked for ``` /login ``` request.

   <img width="1918" height="1137" alt="image" src="https://github.com/user-attachments/assets/98cb2da0-acdd-4c0c-ba28-c5f5a3033a31" />

- Sent this to Intruder as we need to do bruteforce attack for getting the username and password.
- After sending, highlighted the username parameter ``` carlos ``` and clinked on ``` Add$$ ``` which marked that and prepared for attack.
- Pasted the ``` Candidate username ``` list in the Payload config section.

   <img width="1917" height="1199" alt="Screenshot 2025-12-29 150936" src="https://github.com/user-attachments/assets/c220058f-e2b6-48f4-8631-e790545377e2" />

- Started the attack.
- After attack finished, I analyzed the result and under the Length column I got all same lengths as ``` 3248 ``` but one username ``` atlas ``` had ``` 3250 ```.
- When I compared that with other usernames, I saw atlas had ``` Incorrect password ``` and other had ``` Incorrect username ```.
- Got to know that ``` atlas ``` might be the potential username.

   <img width="1861" height="1113" alt="Screenshot 2025-12-29 150758" src="https://github.com/user-attachments/assets/af7464d9-bb08-4884-b9c2-a08916e96aa1" />

- Now, password has to bruteforced, so I marked password parameter now in the same way as I did for username.
- Pasted the ``` Candidate Passwords ``` in the Payload config section and started the attack.

  <img width="1919" height="1199" alt="Screenshot 2025-12-29 150840" src="https://github.com/user-attachments/assets/d86fa521-15e5-4513-acfa-6730acbaea88" />

- After attack finished, I got three lengths:
  - 3250
  - 3337
  - 187

    <img width="1863" height="1115" alt="Screenshot 2025-12-29 150821" src="https://github.com/user-attachments/assets/d562b748-9b78-4bd0-b48c-43b602c0dcad" />

- Both ``` 3250 ``` and ``` 3337 ``` responses looked similar, a different response I got was for ``` 187 ``` which had password as ``` jessica ```.
- So, I thought that the potential username -> ``` atlas ``` and password -> ``` jessica ``` should be these.
- Went to login and tried login using credentials and completed the lab.

   <img width="1919" height="1198" alt="Screenshot 2025-12-29 150729" src="https://github.com/user-attachments/assets/567d0264-c38c-4a11-b1a7-822ad3a09567" />

## Concepts Learned from Lab-1
- How to get username and passwords by bruteforcing using wordlists.
- Learned how to take use of Intruder in BurpSuite.

## Resources
- Intruder in BurpSuite.


## Bypassing two-factor authentication
If the user is first prompted to enter a password, and then prompted to enter a verification code on a separate page, the user is effectively in a "logged in" state before they have entered the verification code.
> Occasionally, you will find that a website doesn't actually check whether or not you completed the second step before loading the page.

# Lab-2: 2FA simple bypass
> This lab's two-factor authentication can be bypassed. You have already obtained a valid username and password, but do not have access to the user's 2FA verification code. To solve the lab, access Carlos's account page.<br>
***Your credentials:*** ``` wiener:peter ``` <br>
***Victim's credentials:*** ``` carlos:montoya ```

## Solution:
- Accessed the lab and got usual dashboard.
- Went to ``` My Account ``` and logged in using given credentials ``` wiener:peter ```.
- Got a verification code page asking to enter code.

   <img width="1901" height="1029" alt="Screenshot 2025-12-29 153457" src="https://github.com/user-attachments/assets/22c1575e-693c-4f1f-aebd-bf6d4299d583" />

- Opened ``` Email client ```, it took to the inbox where code was given as ``` 1017 ``` for wiener.
- Now, lab asks to access Carlos' account page to solve the lab, did same for that too.
- Enterd username and password as given and it asked to enter verification code as expected.
- Went to Email client but got nothing, there was no code in the inbox.
- Since, on the previous page, it said that website doesn't actually check whether or not you enter he verification code, when it's asked you are already in the logged-in stage and can acceess logged-in pages.
- So, thought of directly accessing the Carlos' account page.
- Modified URL by typing ``` /my-account ``` after removing ``` /login2 ``` and got the My Account page of Carlos and completed the lab.

   <img width="1919" height="1199" alt="Screenshot 2025-12-29 153810" src="https://github.com/user-attachments/assets/b43e7b42-978b-473d-857a-b9901a202b71" />

## Concepts Learned from Lab-2
- How to bypass 2FA authentication as we are already in the logged in stage.

## Wrong Tangents
- Before thinking to change the URL, was wandering around the ``` Exploit the server ``` tab and got nothing.







   

  



















