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



    

    




























  


   
