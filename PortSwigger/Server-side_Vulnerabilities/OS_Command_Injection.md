# What is OS command injection?
OS command injection is also known as shell injection. It allows an attacker to execute operating system (OS) commands on the server that is running an application, and typically fully compromise the application and its data.

## Useful commands:
<pre><b>Purpose of command</b>        <b>Linux</b>       	<b>Windows</b>
Name of current user:     whoami	     whoami
Operating system:	     uname -a	      ver
Network configuration:   ifconfig 	  ipconfig /all
Network connections:  	netstat -an	   netstat -an
Running processes:        ps -ef	    tasklist</pre>

## Injecting OS commands
A shopping application lets the user view whether an item is in stock in a particular store. This information is accessed via a URL:
```
https://insecure-website.com/stockStatus?productID=381&storeID=29
```
To provide the stock information, the application must query various legacy systems. For historical reasons, the functionality is implemented by calling out to a shell command with the product and store IDs as arguments:
```
stockreport.pl 381 29
```
Consider a command:
```
& echo nklwndlwdnl &
```
If this is submitted in the productID parameter:
```
stockreport.pl & echo nklwndlwdnl & 29
```
This gives output:
```
Error - productID was not provided
nklwndlwdnl
29: command not found
```

``` echo ``` -> echoes out the text entered after this command
``` & ``` -> seprates two or more shell commands and let them execute simultaneously

> Placing the additional command separator ``` & ``` after the injected command is useful because it separates the injected command from whatever follows the injection point.

This reduces the chance that what follows will prevent the injected command from executing.

# Lab: OS command injection, simple case
> This lab contains an OS command injection vulnerability in the product stock checker.<br>
The application executes a shell command containing user-supplied product and store IDs, and returns the raw output from the command in its response.<br>
To solve the lab, execute the ``` whoami ``` command to determine the name of the current user.

## Solution:
- Accessed the lab and got usual dashboard.
- Opened a product and checked its stock.
- Opened Burp and got ``` /product/stock ``` POST request and sent it to the Repeater.

   <img width="1919" height="1199" alt="Screenshot 2025-12-31 163359" src="https://github.com/user-attachments/assets/caa9cdc0-2276-4aea-b07d-f3eed3751fae" />

- Appended ``` |whoami ``` after the ``` productId & storeId ```.

   <img width="1919" height="1199" alt="Screenshot 2025-12-31 163345" src="https://github.com/user-attachments/assets/f7709cb3-0150-427a-ba21-396e3212cc14" />

- Completed the lab.

   <img width="1914" height="1198" alt="Screenshot 2025-12-31 163330" src="https://github.com/user-attachments/assets/640ad3ac-43eb-4bd4-858c-28ee974af419" />

## Concepts Learned:
- Learned about manipulating a web server application using OS command injections.

## Wrong Tangets:
- As the lab described to use ``` whoami ``` and get the username, I was appending whoami at POST line -> ``` /product/stock/whoami ```.
- Was trying to modify URL by adding whoami.













