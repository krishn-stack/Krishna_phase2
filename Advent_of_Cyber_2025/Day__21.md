# Malware Analysis - Malhare.exe
 > Learn about malware analysis and forensics.

## Task 1 -> Introduction
 > And in our kingdom of Wareville, just like in others, thousands of files of all kinds pass through the systems every day, from DOCX, PDF resumes received by our elves, to financial spreadsheets, CSVs from the accounting department, and executable files launched by different applications. But have you ever wondered which of these might be malicious? Which ones could actually belong to King Malhare? An interesting question, isn’t it?

- ``` My AttackBox has started and I am ready to learn about malware analysis. ``` marks the completion of Task 1.

## Task 2 -> Malware Analysis
### HTA File Structure
An HTA file usually contains three main parts:

1. ***The HTA declaration:*** This defines the file as an HTML Application and can include basic properties like title, window size, and behaviour.
2. ***The interface (HTML and CSS):*** This section creates the layout and visuals, such as buttons, forms, or text.
3. ***The script (VBScript or JavaScript):*** Here is where the logic lives; it defines what actions the HTA will perform when opened or when a user interacts with it.

   <img width="1551" height="720" alt="image" src="https://github.com/user-attachments/assets/38ace255-ba06-4f16-80be-f909c88f514c" />

 We can see three key variables: $U, $C, and $B. Let’s quickly break down what each does:

1. ***$U:*** Holds the decoded URL, the location from which the next script or payload will be fetched.
2. ***$C:*** Stores the content downloaded from that URL, usually a PowerShell script or text instructions.
3. ***$B:*** Converts that content into an executable scriptblock and runs it directly in memory.

## Solution:
- Opened ``` survey.hta ``` file using pluma and by running command ``` pluma /root/Rooms/AoC2025/Day21/survey.hta ```
- Saw 5 funnctions:
  - ***window_onLoad:*** This function will autmatically execute when the HTA loads and executes the ```getQuestions()``` function.
  - ***getQuestions():*** This function makes some external requests and then ultimately runs the ```decodeBase64``` function and calls the ```provideFeedback``` function with the data.
  - ***provideFeedback(feedbackString):*** This function gathers some data about the computer, makes some external requests, and then ultimately executes something we still need to analyse.
  - ***decodeBase64(base64):*** This function takes in a base64 string and converts it into binary.
  - ***RSBinaryToString(xBinary):*** This function takes binary input and converts it back into a string.
- Analysed the .hta file according to the questions asked and got the answers and flag.

## Answers and Flag:
- ***What is the title of the HTA application?***
  ```
  Best Festival Company Developer Survey
  ```
- ***What VBScript function is acting as if it is downloading the survey questions?***
  ```
  getQuestions
  ```
- ***What URL domain (including sub-domain) is the "questions" being downloaded from?***
  ```
  survey.bestfestiivalcompany.com
  ```
- ***Malhare seems to be using typosquatting, domains that look the same as the real one, in an attempt to hide the fact that the domain is not the inteded one, what character in the domain gives this away?***
  ```
  i
  ```
- ***Malicious HTAs often include real-looking data, like survey questions, to make the file seem authentic. How many questions does the survey have?***
  ```
  4
  ```
- ***Notice how even in code, social engineering persists, fake incentives like contests or trips hide in plain sight to build trust. The survey entices participation by promising a chance to win a trip to where?***
  ```
  South Pole
  ```
- ***The HTA is enumerating information from the local host executing the application. What two pieces of information about the computer it is running on are being exfiltrated? You should provide the two object names separated by commas.***
  ```
  ComputerName,UserName
  ```
- ***What endpoint is the enumerated data being exfiltrated to?***
  ```
  /details
  ```
- ***What HTTP method is being used to exfiltrate the data?***
  ```
  GET
  ```
- ***After reviewing the function intended to get the survey questions, it seems that the data from the download of the questions is actually being executed. What is the line of code that executes the contents of the download?***
  ```
  runObject.Run "powershell.exe -nop -w hidden -c " & feedbackString, 0, False
  ```
- ***It seems as if the malware site has been taken down, so we cannot download the contents that the malware was executing. Fortunately, one of the elves created a copy when the site was still active. Download the contents from here. What popular encoding scheme was used in an attempt to obfuscate the download?***
  ```
  base64
  ```
- ***Decode the payload. It seems as if additional steps where taken to hide the malware! What common encryption scheme was used in the script?***
  ```
  rot13
  ```
- ***Either run the script or decrypt the flag value using online tools such as CyberChef. What is the flag value?***
  ```
  THM{Malware.Analysed}
  ```
  
