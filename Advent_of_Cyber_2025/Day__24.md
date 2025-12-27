# Exploitation with cURL - Hoperation Eggsploit
 > The evil Easter bunnies operate a web control panel that holds the wormhole open. Using cURL, identify the endpoints, send the required requests, and shut the wormhole once and for all.

## Task 1 -> Introduction
> According to blue-team intel, the wormhole is held open by a control panel on the Evil Bunnies' web server. The team must shut it down first to cut off reinforcements before facing King Malhare.

> However, the terminal they have is bare. No Burp Suite, no browser, just a command prompt.

> But that's fine. The team will use the command line and cURL to speak HTTP directly: send requests, read responses, and find the endpoints that shut the portal.

- ``` I have successfully started the AttackBox and the target machine! ``` marks the completion of Task 1.

## Task 2 -> Web Hacking Using cURL
### HTTP Requests Using cURL
 > Applications, like our browsers, communicate with servers using HTTP (Hypertext Transfer Protocol). Think of HTTP as the language for asking a server for resources (pages, images, JSON data) and getting answers back.

> So if you want to access a website, your browser sends an HTTP request to the web server. If the request is valid, the server replies with an HTTP response that contains the data needed to display the website.

> In the absence of a browser, you can still speak HTTP directly from the command line. The simplest way is with cURL.

> ``` curl ``` is a command-line tool for crafting HTTP requests and viewing raw responses. It's ideal when you need precision or when GUI tools aren't available.

## Solution:
- Ran ``` curl http://MACHINE_IP/ ```.
- Then ran ``` curl -i -X POST -d "username=admin&password=admin" http://MACHINE_IP/post.php ``` and got 1st flag.
- Ran ``` curl -c cookies.txt -d "username=admin&password=admin" http://MACHINE_IP/cookie.php ``` after that ``` curl -b cookies.txt http://MACHINE_IP/cookie.php ``` and got the flag.
- Made ``` passwords.txt ``` file using touch command and write into it using ```nano``` text editor.
- Made ``` loop.sh ``` file using same method and written into it the given code.
- Using ``` chmod +x loop.sh ``` command made this file executable.
- Ran this file and got password.
- Make a request to ``` user-agent ``` using command ``` curl -i -A "TBFC" http://MACHINE_IP/agent.php ``` and got the flag.

  ## Flags:
  ```
  THM{curl_post_success}
  THM{session_cookie_master}
  secretpass
  THM{user_agent_filter_bypassed}
  ```
  

