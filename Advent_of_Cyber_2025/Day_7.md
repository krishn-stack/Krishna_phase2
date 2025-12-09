# Network Discovery - Scan-ta Clause
  > Discover how to scan network ports and uncover what is hidden behind them.

## Task 1 -> Introduction:
  > Christmas preparations are delayed - HopSec has breached our QA environment and locked us out! Without it, the TBFC projects can't be tested, and our entire SOC-mas pipeline is frozen. To make things worse, the server is slowly transforming into a twisted EAST-mas node.
Can you uncover HopSec's trail, find a way back into tbfc-devqa01, and restore the server before the bunny's takeover is complete? For this task, you'll need to check every place to hide, every opened port that bunnies left unprotected. Good luck!

- ``` I have successfully launched the target machine and the AttackBox. ``` marks the completion of Task 1.

## Task 2 -> Discover Network Services
### Discovering Exposed Services:
   > Although we lost access to the QA server, at least it's still active, and we know its IP address. That's good news, since now we can counterattack and hopefully find our way back. Ensure you understand basic Networking Concepts like network ports, and let's plan the engagement!
   > 1. Know your target. In our case, it is the ``` tbfc-devqa01 ``` server with the ``` MACHINE_IP ``` IP address.
   > 2. Scan the IP for open ports, especially common ones like 22 for SSH and 80 for HTTP.
   > 3. Explore what's behind the open ports, maybe it's a vulnerable web server running on port 80.
   > 4. Exploit the exposed service, find a way in, and kick out the bad bunnies from the QA server.

   > Along the practical of today's task you will find three keys.
Keep note of them since you will later need them for the web app.
The format will be ``` KEYNAME:KEY ```.


## Answers and Flags:
- What evil message do you see on top of the website?
  > Pwned by HopSec
- What is the first key part found on the FTP server?
  > 3aster_
- What is the second key part found in the TBFC app?
  > 15_th3_
- What is the third key part found in the DNS records?
  > n3w_xm45
- Which port was the MySQL database running on?
  > 3306
- Finally, what's the flag you found in the database?
  > THM{4ll_s3rvice5_d1sc0vered}

## Concepts Learned:
- Learned about new commands ``` nmap ```, ``` ftp ```.
- Learned about new port ``` UDP ```

## Solution:
### The Simplest Port Scan
  > There are many tools you can use to scan for open ports, from preinstalled Netcat on Linux and PowerShell on Windows, to specialized, powerful tools like Nmap and Naabu. Let's use Nmap for this task and perform a basic scan from the AttackBox or your own VPN-connected attacking machine.

   - To scan open ports, used nmap command ``` nmap MACHINE_IP ```.
   - Got 2 open ``` TCP ports ```
       - 22/tcp
       - 80/tcp
   - Opened https://MACHINE_IP on Firefox and got a site opened which was taken over by bunnies.
     
        <img width="1853" height="802" alt="image" src="https://github.com/user-attachments/assets/fc9a032e-e98f-47df-a847-6f7504a15aea" />

### Scanning Whole Range
   - For scanning, used ``` nmap -p- --script=banner MACHINE_IP ``` command because previously we did onyl for 1000 ports but now we did scanning for all open ports in the server.
   - We got 2 more open ports other than previous ones ->
     - 21212/tcp
     - 25251/tcp
   - Saw there is onr port which is running on the ``` ftp ``` server, so tried to access it using the ftp command.
   - Used ``` ftp MACHINE_IP 21212 ``` command, entered name as ``` anonymous ```, entered into ftp, used ls command to get list of things in the server.
   - There got ``` tbfc_qa_key1 ``` which we want, so used ``` get tbfc_qa_key1 ``` command and got first key as ``` 3aster_ ```
   - Since we don't know on which server the second port is running, used ``` netcat (nc) ``` command to link to the network.
   - Used ``` nc -v MACHINE_IP 25251 ``` and got second key as ``` 15_th3_ ```.
   - We know that we have 2 types of ports ``` TCP ``` and ``` UDP ```, another transfer protocol and we have only scanned TCP ones.
   - Now to switch on to the UDP ones, used ``` nmap -sU MACHINE_IP ``` and got another open port ``` 53/udp ``` which was associated with DNS.
     > DNS -> a protocol that drives modern web by connecting domains to IPs.
   - To search for the third key, used ``` dig ``` command as ``` dig @MACHINE_IP TXT key3.tbfc.local +short ``` and got the third key ``` n3w_xm45 ```.

### On-Host Service Discovery
   - Now, I have all the keys so I went to Firefox to unlock the server, entered all the keys and unlocked it.
   - Went to the open terminal and used ``` ss -tunlp ``` command and got whole list of existing ports in the form of a table.
   - Used a sql query to find the flag.
     
      ``` mysql -D tbfcqa01 -e "select * from flags;" ```
     
     
     
