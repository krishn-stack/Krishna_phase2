# Web Attack Forensics - Drone Alone
 > Explore web attack forensics using Splunk.

## Task 1 -> Introduction
 > TBFC’s drone scheduler web UI is getting strange, long HTTP requests containing Base64 chunks. Splunk raises an alert: “Apache spawned an unusual process.” On some endpoints, these requests cause the web server to execute shell code, which is obfuscated and hidden within the Base64 payloads. For this room, your job as the Blue Teamer is to triage the incident, identify compromised hosts, extract and decode the payloads and determine the scope.

> You’ll use Splunk to pivot between web (Apache) logs and host-level (Sysmon) telemetry.

> Follow the investigation steps below; each corresponds to a Splunk query and investigation goal.

- ``` I have successfully started the AttackBox and the target machine! ``` marks the completion of Task 1.

## Task 2 -> Web Attack Forensics
 ### Solution:
 - Opened ``` http://MACHINE_IP:8000 ``` site and logined using the given credentials.
 - Started to analyze using Splunk.

    <img width="1020" height="580" alt="image" src="https://github.com/user-attachments/assets/eb7f2bb1-8a21-42e2-9367-33322e2eefdc" />

 - Used given query and got two logs, from which the first one has a ``` base64 ``` encoded text -> ``` VABoAGkAcwAgAGkAcwAgAG4AbwB3ACAATQBpAG4AZQAhACAATQBVAEEASABBAEEASABBAEEA ```
   ```
   index=windows_apache_access (cmd.exe OR powershell OR "powershell.exe" OR "Invoke-Expression") | table _time host clientip uri_path uri_query status
   ```
 - Decoded that text and got ``` T�h�i�s� �i�s� �n�o�w� �M�i�n�e�!� �M�U�A�H�A�A�H�A�A� ```.
 - Next query used, changed view to ``` Raw ``` and analyzed the logs and got ``` powershell.exe ``` which we needed to find as an error message.
   ```
   index=windows_apache_error ("cmd.exe" OR "powershell" OR "Internal Server Error")
   ```

     <img width="2924" height="908" alt="image" src="https://github.com/user-attachments/assets/218ea463-6b0a-4301-9cc1-fb3dcf21b434" />
 
 - Next Query used, changed view to ``` Table ``` and analyzed.
   ```
   index=windows_sysmon ParentImage="*httpd.exe"
   ```
   If results show child processes such as:

   ``` ParentImage = C:\Apache24\bin\httpd.exe ```
   
   ``` Image = C:\Windows\System32\cmd.exe ```
   
   It indicates a successful command injection where Apache executed a system command.

    <img width="2928" height="1184" alt="image" src="https://github.com/user-attachments/assets/1045bd35-9ed8-475b-b2e9-1e605fed63a7" />


 - Next query used.
   ```
   index=windows_sysmon *cmd.exe* *whoami*
   ```

      <img width="2922" height="1288" alt="image" src="https://github.com/user-attachments/assets/851e7997-fb4e-4ee0-ba9e-25c6a128a6c3" />

 - Last query used was but no results were found for it. 
   ```
   index=windows_sysmon Image="*powershell.exe" (CommandLine="*enc*" OR CommandLine="*-EncodedCommand*" OR CommandLine="*Base64*")
   ```

      <img width="2914" height="562" alt="image" src="https://github.com/user-attachments/assets/4558fd50-0d6b-4ac0-9b0b-e57a1a0690f9" />

 ## Answers:
 - What is the reconnaissance executable file name?
   ```
   whoami.exe
   ```
 - What executable did the attacker attempt to run through the command injection?
   ```
   PowerShell.exe
   ```
   

       


    
    
   

