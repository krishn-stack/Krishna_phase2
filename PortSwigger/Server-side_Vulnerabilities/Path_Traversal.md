# Path Traversal
  > Path Traversal is also known as Directory Traversal. It can be used to read arbitary files from the server that is running on the server.

  > It can include:
> 1. Application code and data
> 2. Credentials login from back-end
> 3. Sensitive Operating System files

- ***This vulnerability seldom allows an attacker to write or change the data of the arbitary files running on the server and allows them to change data and behaviour of the web application on the server***.

## How to read arbitary files using Path Traversal?
  > Imagine a shopping application that displays images of items for sale. This might load an image using the following HTML:
```
<img src="/loadImage?filename=218.png">
```
- In this ``` loadImage ``` takes a filename as parameter and returns the contents in the file.
> The image files are stored on disk in the location /var/www/images/. To return an image, the application appends the requested filename to this base directory and uses a filesystem API to read the contents of the file.

- It means that loadImage URL reads the following path:
  ```
   /var/www/images/218.png
  ```
 > This application implements no defenses against path traversal attacks. As a result, an attacker can request the following URL to retrieve the /etc/passwd file from the server's filesystem:
```
https://insecure-website.com/loadImage?filename=../../../etc/passwd
```
- This indicates that path read by the server:
  ```
  /var/www/images/../../../etc/passwd
  ```
- ``` ../ ``` , a command used to go back from the current directory to the previous directory.
- So, by ``` ../../../ ``` means to back to the root directory as server reads files from ``` /var/www/images/218.png ``` and ``` etc/passwd ``` is the file from which we need to extract data.


# Lab -> File path traversal, simple case
  > This lab contains a path traversal vulnerability in the display of product images.
> To solve the lab, retrieve the contents of the /etc/passwd file.

## My Solve:
- Opened the Burp Suite, Accessed the lab in it.
- It showed a product website.
- Opened Burp suite tracker, sent the first product into Repeater.
- Opened Repeater section and got this:
  
    <img width="1897" height="1108" alt="image" src="https://github.com/user-attachments/assets/610bed2d-4c7a-48b9-a192-afdc28ddaae0" />
    
- Tried typing ``` /etc/passwd ``` and sent the request and got nothing.
  
    <img width="1471" height="895" alt="Screenshot 2025-12-22 201416" src="https://github.com/user-attachments/assets/0fa1648c-3c21-4566-a1da-b047bf42370b" />

- Since, ``` etc/passwd ``` file was not present in the current directory, I had to move to the root directory from ``` /var/www/images/some.png ```, I changed ``` GET /product?productId=1 HTTP/2 ``` to ``` GET /image?filename=../../../../etc/passwd HTTP/2 ```.
- Sent the request and as a response got the the file and completed the lab.

    <img width="1903" height="1111" alt="Screenshot 2025-12-22 201254" src="https://github.com/user-attachments/assets/24b4ba9b-bc6b-412f-8c28-f2ce6cf3271d" />


