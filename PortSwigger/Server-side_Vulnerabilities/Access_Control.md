# What is Access Control ?
  > Access Control is the application of constraints on who or what is authorised to perform actions or access resources.

In the context of web applications, access control is dependent on authentication and session management:
 - ***Authentication*** confirms that the user is who they say they are.
 - ***Session management*** identifies which subsequent HTTP requests are being made by that same user.
 - ***Access control*** determines whether the user is allowed to carry out the action that they are attempting to perform.

Access Control vulnerability allows an attacker to manipulate the web application to believe that he is what he is not and could access the resources of web application which he is not allowed to.

# Vertical Priviledge Escalation
If an attacker tries to gain access of a user's functionality and could access their resources which he should not be permitted to access (e.g. administrator), then this is called ***Vertical Priviledge Escalation***.

## 1. Unprotected functionality
In this, vertical priviledge escalation arises when web application does not enforce any kind of security/protection for sensitive information or functionality. If this happens it's called ***Unprotected Functionality***.

***For example:***
- ```
  https://insecure-website.com/admin
  ```
Sometimes, this sensitive admin functionality is hosted somewhere else instead of directly in admin.

- ```
   https://insecure-website.com/robots.txt
  ```

## Lab-1: Unprotected admin functionality
  > This lab has an unprotected admin panel.<br>
Solve the lab by deleting the user ``` carlos ```.

### Solution:
- Accessed the lab, got below dashboard.

    <img width="1919" height="1199" alt="Screenshot 2025-12-28 163426" src="https://github.com/user-attachments/assets/d56c5dfc-4c32-4ff3-9a59-a5fbe0279f26" />

- Tried changing the URL by appending ``` /admin ``` at the last of it but didn't work and got this page.

    <img width="1919" height="1197" alt="Screenshot 2025-12-28 163443" src="https://github.com/user-attachments/assets/97719aff-1d16-40cd-93c9-f7fffc900722" />

- Then tried appending with ``` /robots.txt ``` and got the direct location of administrative functionality -> ``` /administrative-panel ```.

    <img width="1919" height="1199" alt="Screenshot 2025-12-28 163459" src="https://github.com/user-attachments/assets/68398f04-d84d-4da6-8f9f-98695b137eaa" />

- Appended ``` /administrative-panel ``` in the dashboard URL, got admin panel.
    
    <img width="1919" height="1192" alt="Screenshot 2025-12-28 163521" src="https://github.com/user-attachments/assets/e9f16f62-c223-4a9f-a299-0c5d22ce6261" />

- Deleted ``` carlos ``` from users and solved the lab.

    <img width="1919" height="1197" alt="Screenshot 2025-12-28 163542" src="https://github.com/user-attachments/assets/d55ea94c-b45f-460f-a0b0-f77a4f4976f8" />

## Concepts Learned from Lab-1
- How to get adminitrative controls by making slight changes to the URL.
- Administrative controls can be on different locations which makes it slightly difficult for attackers to guess the exact location.
- These locations can be found by brute-forcing.

## 2. Unprotected functionality - continued....
Sometimes sensitive administrative functionality is made by concealing it into less predictable URL. This is an example of ``` security by obscurity ```
***For example***
```
https://insecure-website.com/administrator-panel-yb556
```
This type of URLs are less predicted by attackers but it can still be known by analyzing it's Inspect view because sometimes it can be hidden in the JavaScript that builds the user-interface and is visible to everyone irrespective of their roles. 
```
<script>
	var isAdmin = false;
	if (isAdmin) {
		...
		var adminPanelTag = document.createElement('a');
		adminPanelTag.setAttribute('href', 'https://insecure-website.com/administrator-panel-yb556');
		adminPanelTag.innerText = 'Admin panel';
		...
	}
</script>
```

## Lab-2: Unprotected admin functionality with unpredictable URL
 > This lab has an unprotected admin panel. It's located at an unpredictable location, but the location is disclosed somewhere in the application.<br>
Solve the lab by accessing the admin panel, and using it to delete the user ``` carlos ```.

## Solution:
- Accessed the lab and got this dashboard.

   <img width="1919" height="1199" alt="Screenshot 2025-12-28 163426" src="https://github.com/user-attachments/assets/fa155f6f-63f1-4834-ac4a-655a9d893d4f" />

- Opened the Inspect view, analyzed the ``` JavaScript ``` code of the web page and got this.

    <img width="1916" height="1199" alt="Screenshot 2025-12-28 164147" src="https://github.com/user-attachments/assets/cc3fe1cb-3fb2-40ff-89d0-832cf2e99c02" />

- Appended ``` /admin-ed2yr4 ``` at the end of the URL and got the Admin panel.

    <img width="1919" height="1197" alt="Screenshot 2025-12-28 164210" src="https://github.com/user-attachments/assets/b86d4d1c-4dc5-419b-9ea9-391509151c83" />

- Deleted ``` carlos ``` from users and solved the lab-2.

    <img width="1917" height="1190" alt="Screenshot 2025-12-28 164226" src="https://github.com/user-attachments/assets/6cf3ef9d-6044-4b66-bcb3-8f3457cb3a6c" />

## Concepts Learned from Lab-2
- Sensitive adminitrative functionality can be concealed in a very unpredictable way.
- Sometimes analyzing JavaScript can get us the location of these functionality.

## 3. Parameter-based access control methods
 > Some applications determine the user's access rights or role at login, and then store this information in a user-controllable location.

This could be:
- A hidden field.
- A cookie.
- A preset query string parameter.

This type of access control vulnerability works well on some unpredictable parameters appened to the URL after login.
***For example:***
```
https://insecure-website.com/login/home.jsp?admin=true
https://insecure-website.com/login/home.jsp?role=1
```
## Lab-3: User role controlled by request parameter
 > This lab has an admin panel at ``` /admin ```, which identifies administrators using a forgeable cookie.<br>
Solve the lab by accessing the admin panel and using it to delete the user ``` carlos ```.<br>
You can log in to your own account using the following credentials: ``` wiener:peter ```.
   
## Solution:
- Accessed the lab and got the usual dashboard.
- Appended ``` /admin ``` as asked in the lab description but didn't get anything.
- Went to ``` My Account ``` and logged in using the credentials.
- A web page asking to update email comes up.
- As it says using a forgeable cookie, so thought of using ``` BurpSuite ```.
- Opened it and looked for something related to ``` login ``` and got this.

    <img width="1918" height="1199" alt="Screenshot 2025-12-28 180850" src="https://github.com/user-attachments/assets/87ad4eac-89ce-4897-9984-b7aacfc21882" />

- In the Request section, saw ``` Admin:false ``` in the Cookie, so tried to make it true.
- Sent ``` /my-account?id=wiener ``` request to repeater.

    <img width="1917" height="1198" alt="Screenshot 2025-12-28 180929" src="https://github.com/user-attachments/assets/72fe5f8c-51fa-4cca-be17-2caa25a35703" />

- Changed admin parameter to ``` Admin:true ``` and sent the request and got the response.

    <img width="1919" height="1199" alt="Screenshot 2025-12-28 180954" src="https://github.com/user-attachments/assets/54896799-3675-4c2b-b30c-5edaa2a2b2f3" />

- Opened Cookies section in the Inspect view and saw it has an ``` Admin ``` cookie with value -> ``` false ```.

    <img width="1919" height="1199" alt="Screenshot 2025-12-28 181040" src="https://github.com/user-attachments/assets/fa830081-de85-4fc8-a30e-faba47d4a8b7" />

- Changed that to true, reloaded the web page, got Admin Panel.
- Deleted ``` carlos ``` from users and completed the lab-3.

    <img width="1919" height="1199" alt="Screenshot 2025-12-28 181101" src="https://github.com/user-attachments/assets/07787809-caf4-4cdf-a57b-5ba50cd71faa" />

## Concepts Learned from Lab-3
- Using Burp how to manipulate admin cookies.
- How to get access control of administrator after logging in into the website as a user.

## Resources:
- BurpSuite

## Wrong Tangets:
- Trying to appending parameters ``` admin=true ``` and ``` role=1/2/3.... ``` at the login page as given in the examples:
  - https://insecure-website.com/login/home.jsp?admin=true
  - https://insecure-website.com/login/home.jsp?role=1


# Horizontal privilege escalation
 > Horizontal privilege escalation occurs if a user is able to gain access to resources belonging to another user, instead of their own resources of that type.

Horizontal privilege escalation attacks may use similar types of exploit methods to vertical privilege escalation. For example, a user might access their own account page using the following URL:
```
https://insecure-website.com/myaccount?id=123
```
By editing the ``` id ``` parameter, attacker can access resources of any user.<br>
***This is an example of IDOR vulnerability ``` (Insecure Direct Object Reference) ```***.<br>
Instead of numbers as id, id parameter can also hold any globally-unique identifiers (GUIDs) making it difficult for an attacker to access resources of different users.

## Lab-4: User ID controlled by request parameter, with unpredictable user IDs
 > This lab has a horizontal privilege escalation vulnerability on the user account page, but identifies users with GUIDs.<br>
To solve the lab, find the GUID for ``` carlos ```, then submit his API key as the solution.<br>
You can log in to your own account using the following credentials: ``` wiener:peter ```.

## Solution:
- Accessed the lab, and got this blog dashboard.

    <img width="1917" height="1197" alt="image" src="https://github.com/user-attachments/assets/459c0223-a6b8-421f-a1bc-31e0925753b1" />

- Logged into the account using given credentials and got this web page.

    <img width="1918" height="1137" alt="image" src="https://github.com/user-attachments/assets/7222f22f-84dd-4c2d-aae2-fca76652b781" />

- Got this ``` id -> 22f2375d-51e0-4932-bd5e-5fed2172ba2d ``` for user ``` wiener ``` but we want for ``` carlos ``` to get his API key.
- Went back to Home to check if I get any blog writen by carlos and got one.
- Opened it but still got ``` postId ``` instead of userId.

   <img width="1919" height="1193" alt="Screenshot 2025-12-28 190429" src="https://github.com/user-attachments/assets/ef147c3b-8fe5-4ed4-b3f2-f4822e2804a0" />

- Clicked on carlos in the above image and got the userId in the URL.

   <img width="1919" height="1199" alt="Screenshot 2025-12-28 190402" src="https://github.com/user-attachments/assets/955bf8d0-0a01-4515-8734-c29a88974645" />

- Went back to ``` My Account ``` and changed wiener's id with carlos' id and got his API key.

   <img width="1919" height="1199" alt="Screenshot 2025-12-28 190341" src="https://github.com/user-attachments/assets/a08ba6f6-5149-4854-9d1a-fb7df710aaf9" />

- Submitted it and completed Lab-4.

   <img width="1917" height="1198" alt="Screenshot 2025-12-28 191413" src="https://github.com/user-attachments/assets/669414bc-873a-490f-b920-d1960200e4ac" />

## Concepts Learned from Lab-4
- Got to know about IDOR and how to access other users information my id modification.

# Horizontal to vertical privilege escalation
 > A Horizontal Priviledge Escalation might allow an attacker to reset or capture the password belonging to another user. If the attacker targets an administrative user and compromises their account, then they can gain administrative access and so perform Vertical Privilege Escalation.

An attacker might be able to gain access to another user's account page using the parameter tampering technique already described for horizontal privilege escalation:
```
https://insecure-website.com/myaccount?id=456
```
If the targeted user is administrator then attacker can get access to sensitive functionality which he shouldn't get.

## Lab-5: User ID controlled by request parameter with password disclosure
> This lab has user account page that contains the current user's existing password, prefilled in a masked input.<br>
To solve the lab, retrieve the administrator's password, then use it to delete the user ``` carlos ```.<br>
You can log in to your own account using the following credentials: ``` wiener:peter ```.

## Solution:
- Accessed the lab and got as usual dashboard.
- Opened Login page and logged in using given credentials and got this.

   <img width="1897" height="1088" alt="image" src="https://github.com/user-attachments/assets/e81b5097-8170-4b8f-abf2-331cc8794f87" />

- Changed the id in the URL from :
  - ``` wiener ``` -> ``` admin ```  (didn't work)
  - ``` wiener ``` -> ``` administrative-panel ```  (didn't work)
  - ``` wiener ``` -> ``` administrator ```  (worked)<br>
and got this.

   <img width="1918" height="1199" alt="Screenshot 2025-12-28 191521" src="https://github.com/user-attachments/assets/66ccc713-e21b-46dd-b4cb-b1d0b841d4d1" />

- Now I need to get the password unmasked so that I could login as administrator.
- Tried to copy the masked password and tried to login but didn't work as password was not getting copied in the first place.
- Opened Burp and saw the ```/administrator ``` request and in response got the password value unmasked.

   <img width="1919" height="1199" alt="Screenshot 2025-12-28 191456" src="https://github.com/user-attachments/assets/fc36d48a-80fb-4e37-9ca2-80c7e58078c0" />

- Logged in as administrator using password, went to Admin Panel.
- Deleted ``` carlos ``` from users and completed the lab.

   <img width="1918" height="1199" alt="Screenshot 2025-12-28 191521" src="https://github.com/user-attachments/assets/5b3129b1-a995-4df2-a199-1bc574253296" />

## Concepts Learnerd from Lab-5
- How to use Horizontal and vertical priviledge escalation together.
    


   
