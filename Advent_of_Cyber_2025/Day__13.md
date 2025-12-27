# YARA Rules - YARA mean one!
   > Learn how YARA rules can be used to detect anomalies.

## Task 1 -> Introduction
 > When McSkidy went missing, there was chaos and uncertainty at The Best Festival Company (TBFC). However, even in her disappearance, McSkidy was trying to help the TBFC blue team. Taking a page out of the crisis communication process, McSkidy sent what looks like a bunch of images to the blue team from an anonymous location. These images looked like they were related to Easter preparations, but they contained a message sent by McSkidy. The crisis communication process outlines that a message might be sent through a folder of images containing hidden messages that can be decoded if you know the keyword. The blue team has to create a YARA rule that runs on the directory containing the images. The YARA rule must trigger on a keyword followed by a code word. After extracting all the code words in ascending order, the blue team will be able to decode the message.

- ``` Let's go! ``` marks the completion of Task 1.

## Task 2 -> Yara Rules
### YARA
   > YARA is a tool built to identify and classify malware by searching for unique patterns, the digital fingerprints left behind by attackers. Imagine it as a detective’s notebook for cyber defenders: instead of dusting for prints, YARA scans code, files, and memory for subtle traces that reveal a threat’s identity.

### Why to use YARA and when to use
  > In the world of cyberattacks, defenders face an endless stream of alerts, suspicious files, and anomalous network fragments. Not every threat stands out; some hide in plain sight, disguised as harmless documents or scripts. That's where YARA shines.
YARA gives defenders the power to detect malware by its behavior and patterns, not just by name. YARA allows you to define your own rules, providing your own view of what constitutes "malicious" behavior.

***Advantages of YARA:***
- ***Speed:*** quickly scans large sets of files or systems to identify suspicious ones.
- ***Flexibility:*** detects everything from text strings to binary patterns and complex logic.
- ***Control:*** lets analysts define exactly what they consider malicious.
- ***Shareability:*** rules can be reused and improved by other defenders across kingdoms.
- ***Visibility:*** helps connect scattered clues into a clear picture of the attack.

### YARA Rules:
  A YARA rule is built from several key elements:
- ***Metadata:*** information about the rule itself: who created it, when, and for what purpose.
- ***Strings:*** the clues YARA searches for: text, byte sequences, or regular expressions that mark suspicious content.
- ***Conditions:*** the logic that decides when the rule triggers, combining multiple strings or parameters into a single decision.

## Solution:
- The room is given by the images of easter eggs in which McSkidy has hidden a message for the Blue Team.
  ```
  /home/ubuntu/Downloads/easter
  ```
- Crafted my own YARA rule with the help of walkthrough video.
  ```
  rule TBFC_Simple_MZ_Detect
  {
    meta:
        author = "TBFC Krishna"
        description = "Extracts TBFC message fragments sent by McSkidy"
        date = "2025-12-17"

    strings:
       $tbfc_msg = /TBFC:[A-Za-z0-9]+/ ascii                      

    condition:
       $tbfc_msg
  }
  ```
- Used VM text editor ``` nano ``` to write this YARA rule.
- Ran this YARA rule by calling YARA
  ```
  yara -rs /home/ubuntu/TBFC_Simple_MZ_Detect /home/ubuntu/
  ```
- Got the number of images sent by McSkidy in which I found the hidden message sent by McSkidy.

## Answers:
- How many images contain the string TBFC?
  ```
  5
  ```
- What regex would you use to match a string that begins with TBFC: followed by one or more alphanumeric ASCII characters?
  ```
  /TBFC:[A-Za-z0-9]+/
  ```
- What is the message sent by McSkidy?
  ```
  Find me in HopSec Island
  ```


  
