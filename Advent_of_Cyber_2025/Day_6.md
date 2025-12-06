# Malware Analysis - Egg-xecutable
  > Discover some common tooling for malware analysis within a sandbox environment.

## Task 1 -> Introduction:
  > The town of Wareville remains quiet in the middle of the night. While the residents of Wareville are nicely tucked up in bed, blissfully unaware, the SOC team at The Best Festival Company (TBFC) remain alert, poised and ready for whatever may face them.
Monitoring their screens, armed with a freshly poured mug of hot cocoa, the elves of the SOC watch their dashboards diligently. 
Suddenly, the elves receive an email in unison from Elf McClause, Head of Elf Affairs, in their inboxes. It reads:

  <img width="831" height="478" alt="image" src="https://github.com/user-attachments/assets/a7ce0c3b-31c0-4d0e-923e-d23c2a4ce1ee" />

> "Why is Elf McClause working at 3AM?" Screams a member of the SOC team in the background. They're right, something is amiss.
Elf McBlue is immediately suspicious. Their years of experience in the SOC have given them the wisdom not to download "out of the blue" executables. Without McSkidy's wisdom, Elf McBlue takes charge, loading up their malware investigation toolkik - the investigation begins.

- ``` I have access to my sandbox environment! ``` marks the completion of Task 1.

## Task 2 -> Malware Analysis Using Sandboxes:
  ### Principles of Malware Analysis
   > Malware analysis is the process of examining a malicious file to understand its functionality, operation, and methods for defence against it. By analysing a malicious file or application, we can see exactly how it operates, and therefore, know how to prevent it. For example, could the malicious file communicate with an attacker's server? We can block that server.Malware wrecking havoc over TBFC
Could the malicious file leave traces on the machine? We can use these to determine if the malware has ever infected another device. Instead of fearing malware, we can take a proactive approach by translating technical findings into practical defensive measures and understanding how the malware fits into an attacker's techniques.
There are two main branches of malware analysis: static and dynamic. Static analysis focuses on inspecting a file without executing it, whereas dynamic analysis involves execution. We will come to these shortly.

### Sandboxes
  > In cyber security, sandboxes are used to execute potentially dangerous code. Think of this as disposable digital play-pens. These sandboxes are safe, isolated environments where potentially malicious applications can perform their actions without risking sensitive data or impacting other systems.


## Answers and Flags:
```
F29C270068F865EF4A747E2683BFA07667BF64E768B38FBB9A2750A3D879CA33
THM{STRINGS_FOUND}
HKU\S-1-5-21-1966530601-3185510712-10604624-1008\Software\Microsoft\Windows\CurrentVersion\Run\HopHelper
http
```

## Concepts Learned:
- Learned about malware analysis.

## Solution:
### Interactive: Static Analysis
- After starting Target machine, I opened ``` pestudio ``` application and opened ``` HopHelper.exe ``` malware file in it.
- Saw the checksums and got the first answer ``` F29C270068F865EF4A747E2683BFA07667BF64E768B38FBB9A2750A3D879CA33 ```
- After that, I went to strings section, scrolled down till the end and got the flag -> ``` THM{STRINGS_FOUND} ```

### Interactive: Dynamic Analysis
- For Dynamic Analysi, I used ``` Regshot ``` application, used to take the snapshot of the ``` sandbox ``` before and after the execution of the malware file and compare what changes occur after its execution.
- Opened Regshot, selected Desktop and took the ``` 1st shot ```.
- Executed the malicious file ``` HopHelper.exe ```.
- On running this file, all the application logos changes to  ``` Easter eggs ```.
- After it's execution, took the second shot and compared both shots in plain text mode.
- Changes occured are opened on the notepad, searched where HopHelper is in it.
- On analyzing, saw that it was running on RUN directory, so definitely it was modified to justify persistence.
  > HKU\S-1-5-21-1966530601-3185510712-10604624-1008\Software\Microsoft\Windows\CurrentVersion\Run\HopHelper
  
