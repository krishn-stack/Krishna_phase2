# XSS - Merry XSSMas
  > Learn about types of XSS vulnerabilities and how to prevent them.

## Task 1 -> Introduction
  >  After last year's automation and tech modernisation, Santa's workshop got a new makeover. McSkidy has a secure message portal where you can contact her directly with any questions or concerns. However, lately, the logs have been lighting up with unusual activity, ranging from odd messages to suspicious search terms. Even Santa's letters appear to be scripts or random code. Your mission, should you choose to accept it: dig through the logs, uncover the mischief, and figure out who's trying to mess with McSkidy.

- ``` I have successfully started the AttackBox and target machine! ``` marks the completion of Task 1.

## Task 2 -> Leave the Cookies, Take the Payload
 > XSS is a web application vulnerability that lets attackers (or evil bunnies) inject malicious code (usually JavaScript) into input fields that reflect content viewed by other users (e.g., a form or a comment in a blog). When an application doesn't properly validate or escape user input, that input can be interpreted as code rather than harmless text. This results in malicious code that can steal credentials, deface pages, or impersonate users. Depending on the result, there are various types of XSS.  In today’s task, we focus on Reflected XSS and Stored XSS.

### Reflected XSS
 > When you see any changes on the website as soon as a malicious ``` script ```/ ``` javascript ``` code is injected into the original webiste code and vanishes later. It's called ``` Reflected XSS ``` and it is temporary as it vanished later.

> You could act, view information, or modify information that your friend or any user could do, view, or access. It's usually exploited via phishing to trick users into clicking a link with malicious code injected.

### Stored XSS
 > A Stored XSS attack occurs when malicious script is saved on the server and then loaded for every user who views the affected page. Unlike Reflected XSS, which targets individual victims, Stored XSS becomes a "set-and-forget" attack, anyone who loads the page runs the attacker’s script.

### Protecting against XSS
> Each service is different, and requires a well-thought-out, secure design and implementation plan, but key practices you can implement are:

> 1. ***Disable dangerous rendering raths***: Instead of using the innerHTML property, which lets you inject any content directly into HTML, use the textContent property instead, it treats input as text and parses it for HTML.
> 2. ***Make cookies inaccessible to JS***: Set session cookies with the HttpOnly, Secure, and SameSite attributes to reduce the impact of XSS attacks.
> 3. ***Sanitise input/output and encode***:
In some situations, applications may need to accept limited HTML input—for example, to allow users to include safe links or basic formatting. However it's critical to sanitize and encode all user-supplied data to prevent security vulnerabilities. Sanitising and encoding removes or escapes any elements that could be interpreted as executable code, such as scripts, event handlers, or JavaScript URLs while preserving safe formatting.


### Solution:
- Opened the website using the ``` Target Machine ``` I.P address.
- Got below displayed site:

     <img width="2890" height="1698" alt="image" src="https://github.com/user-attachments/assets/5232bf20-8a9b-4ea9-b1ad-210344217153" />

- Firstly I types my name in the search bar, it displayed that.
- Then I ran a malicious script code ``` <script> Reflected('Krishna') </script> ``` and it gave the flag.
- Then went to the second bar given below and applied same thing, firstly typed my name, it displayed my name and stored it as previously searched item i.e. it has injected into the original HTML code of website forever.
- So, got to know that it is related to Stored XSS.
- So, I ran the same malicious code with some changes  ``` <script> Stored('Krishna') </script> ``` and it again gave the flag.


### Answers and Flags:
- Which type of XSS attack requires payloads to be persisted on the backend?<br>
  ```
  stored
  ```
- What's the reflected XSS flag?
  ```
  THM{Evil_Bunny}
  ```
- What's the stored XSS flag?
  ```
  THM{Evil_Stored_Egg}
  ```





























