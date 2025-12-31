# What is SSRF?
 > Server-side request forgery is a web security vulnerability that allows an attacker to cause the server-side application to make requests to an unintended location.
 
 The attacker might cause the server to make a connection to internal-only services within the organization's infrastructure.

 ## 1. SSRF attacks against the server
In an SSRF attack against the server, the attacker causes the application to make an HTTP request back to the server that is hosting the application, via its loopback network interface. This typically involves supplying a URL with a hostname like ``` 127.0.0.1 ``` (a reserved IP address that points to the loopback adapter) or ``` localhost ``` (a commonly used name for the same adapter).

***For example:***
- A shopping application that lets the user view whether an item is in stock in a particular store. To provide the stock information, the application must query various back-end REST APIs. It does this by passing the URL to the relevant back-end API endpoint via a front-end HTTP request. When a user views the stock status for an item, their browser makes the following request:
```
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://stock.weliketoshop.net:8080/product/stock/check%3FproductId%3D6%26storeId%3D1
```

- An attacker can modify the request to specify a URL local to the server:
```
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://localhost/admin
```
> i. An attacker can visit the /admin URL, but the administrative functionality is normally only accessible to authenticated users.<br>
> ii. If the request to the /admin URL comes from the local machine, the normal access controls are bypassed. The application grants full access to the administrative functionality, because the request appears to originate from a trusted location.

SSRF Attacks arise due to the following reasons:
- The access control check might be implemented in a different component that sits in front of the application server. When a connection is made back to the server, the check is bypassed.
- the application might allow administrative access without logging in, to any user coming from the local machine. This provides a way for an administrator to recover the system if they lose their credentials. This assumes that only a fully trusted user would come directly from the server.
- The administrative interface might listen on a different port number to the main application, and might not be reachable directly by users.

# Lab-1: Basic SSRF against the local server
> This lab has a stock check feature which fetches data from an internal system.<br>
To solve the lab, change the stock check URL to access the admin interface at ``` http://localhost/admin ``` and delete the user ``` carlos ```.

## Solution:
- Accessed the lab and got this dashboard.

  <img width="1918" height="1136" alt="image" src="https://github.com/user-attachments/assets/30cee9cc-c984-443c-91e0-20d450041b32" />

- Opened a product and checked it's stock.
- Opened Burp and found ``` /product/stock ``` request in the HTTP history.
- Sent it to Repeater.

    <img width="1919" height="1199" alt="Screenshot 2025-12-30 193036" src="https://github.com/user-attachments/assets/2da4fb0b-2833-4f3b-a869-dffd71943425" />

- Changed ``` stockApi ``` to ``` http://localhost/admin ``` and sent the request.
- Got this response.

     <img width="1912" height="1197" alt="Screenshot 2025-12-30 193115" src="https://github.com/user-attachments/assets/09c6a8ff-8db0-41ca-b019-0d5890a50580" />

- Scrolled and found a path to delete carlos from users -> ``` /deleter?username=carlos ```.
- Appended this to previous stockApi request and sent  the request.

    <img width="1919" height="1199" alt="Screenshot 2025-12-30 192949" src="https://github.com/user-attachments/assets/b3933e73-ff86-45b9-98ed-648700f5a3dc" />

- Got this and completed the lab.

    <img width="1918" height="1199" alt="Screenshot 2025-12-30 192936" src="https://github.com/user-attachments/assets/23c24bd8-2ef5-4a53-b487-b76e50089042" />

## Concepts Learned:
- How to get to another request from another request within the web application server.
  - I mean from checking stock to accessing administrator functionality.

## Wrong Tangents:
- Was trying to access admin functionality by changing URL.

## 2. SSRF attacks against other back-end systems
The application server is able to interact with back-end systems that are not directly reachable by users. These systems often have non-routable private IP addresses. The back-end systems are normally protected by the network topology, so they often have a weaker security posture. In many cases, internal back-end systems contain sensitive functionality that can be accessed without authentication by anyone who is able to interact with the systems.

***An attacker can submit the following request to exploit the SSRF vulnerability, and access the administrative interface:***
```
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://192.168.0.68/admin
```

# Lab-2: Basic SSRF against another back-end system
> This lab has a stock check feature which fetches data from an internal system.<br>
To solve the lab, use the stock check functionality to scan the internal ``` 192.168.0.X ``` range for an admin interface on port ``` 8080 ```, then use it to delete the user ``` carlos ```.

## Solution:
- Accessed the lab and got usual dashboard.

   <img width="1916" height="1132" alt="image" src="https://github.com/user-attachments/assets/fc187910-24d9-460c-9859-d1219c889557" />

- Opened a product and checked its stock.
- Went to Burp and got ``` /product/stock ``` request.

    <img width="1917" height="1132" alt="image" src="https://github.com/user-attachments/assets/a5065efe-c8ce-4ea6-a2ed-de9de11b7c3d" />

- Sent it to Intruder and changed the ``` stockApi ``` to the given I.P address -> ``` http://192.168.0.X:8080/admin ```.

  <img width="1917" height="1137" alt="image" src="https://github.com/user-attachments/assets/5e4ca880-4be3-4504-833a-fceef4140223" />

- As the lab description says that ``` X ``` has to be in range, so I bruteforced it from ``` 1 -> 255 ```.
- In the Payload panel, changed ``` Payload Type ``` to ``` Numbers ``` and entered range.

    <img width="1918" height="1131" alt="image" src="https://github.com/user-attachments/assets/4e20aeda-e754-4912-9462-8e9e4db977ae" />

- Started the Sniper Attack and after finishing the attack, got this.

   <img width="1864" height="1112" alt="Screenshot 2025-12-30 202420" src="https://github.com/user-attachments/assets/84e0f75a-7c34-4614-b91f-1f4e66434d54" />

- I got ``` X -> 218 ```, the only one with different ``` length ``` and along with ``` 200 -> OK ``` status code.
- Now sent it to repeater and sent the request.
- Again got the path to delete carlos from users as ``` delete?username=carlos ```.
- Appended it to the previous request and again sent the request and completed the lab.

   <img width="1919" height="1199" alt="Screenshot 2025-12-30 202402" src="https://github.com/user-attachments/assets/58b17d49-ad93-4b6d-aa80-58bba7a49111" />

## Concepts Learned:
- How to get to know the I.P address by brute forcing it.

  









