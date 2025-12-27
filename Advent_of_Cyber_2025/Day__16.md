# Forensics - Registry Furensics
 > Learn what the Windows Registry is and how to investigate it.

## Task 1 -> Introduction
  > TBFC is under attack. Systems are exhibiting weird behavior, and the company is now feeling the absence of its lead defender, McSkidy. However, McSkidy made sure the legacy continues.

> McSkidy’s team, determined and well-trained, is fully confident in securing all the systems and regaining control before the big event, SOCMAS.

> They have now decided to conduct a detailed forensic analysis on one of the most critical systems of TBFC, dispatch-srv01. The dispatch-srv01 coordinates the drone-based gifts delivery during SOCMAS. However, recently it was compromised by King Malhare’s bandits of bunnies.
 
> TBFC’s defenders have decided to split into specialized teams to uncover the attack on this system through detailed forensics. While some of the other team members investigate logs, memory dumps, file systems, and other artefacts, you will work to investigate the registry of this compromised system.

- ``` I successfully have access to my target machine! ``` marks the completion of Task 1.

## Task 2 -> Investigate the Gifts Delivery Malfunctioning
  ### Windows Registry
   > Your brain knows pretty much everything about you. It's just like a database storing the human configuration.

> Windows OS is not a human, but it also needs a brain to store all its configurations. This brain is known as the ``` Windows Registry ```. The registry contains all the information that the Windows OS needs for its functioning. 

> Now, this Windows brain (Registry) is not stored in one single place, unlike a human brain, which is situated in one single place inside the head. It is made up of several separate files, each storing information on different configuration settings. These files are known as ``` Hives ```.

## Solution:
- Opened ``` Registry Explorer ``` , went to ``` File ``` then ``` Load Hive ``` and opened ``` SYSTEM ``` hive.
- Opened ``` Root -> Microsoft -> Windows -> CurrentVersion -> uninstall file ```.
- Sorted data using Timestamp and got only 1 after 20th and got the first answer as ``` DroneManager Updater ```
- Opened another hive ``` NTUSER.DAT ```.
- Opened ``` Root -> Windows NT -> CurrentVersion -> AppCompatflags -> Compatibility Assistant -> Store ```.
- Got the answer to the swcond question ``` C:\Users\dispatch.admin\Downloads\DroneManager_Setup.exe ```
- Came back to previous hive.
- Opened  ``` Root -> Microsoft -> Windows -> CurrentVersion -> run ```.
- Got answer to the third question ``` C:\Program Files\DroneManager\dronehelper.exe" --background ```

## Answers:
- What application was installed on the ``` dispatch-srv01 ``` before the abnormal activity started?
  ``` DroneManager Updater ```
- What is the full path where the user launched the application (found in question 1) from?
  ``` C:\Users\dispatch.admin\Downloads\DroneManager_Setup.exe ```
- Which value was added by the application to maintain persistence on startup?
  ``` C:\Program Files\DroneManager\dronehelper.exe" --background ```
 


