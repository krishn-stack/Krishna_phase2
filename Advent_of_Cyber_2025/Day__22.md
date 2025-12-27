# C2 Detection - Command & Carol
 > Explore how to analyze a large PCAP and extract valuable information.

## Task 1 -> Introduction
 > The TBFC is very wary since the last series of attacks by the underlings of King Malhare. They are on full alert for anything happening. But they are getting restless; it is too quiet. Sir Elfo of the TBFC takes the initiative and proposes to hunt for Command and Control traffic using the meticulously collected network traffic. A majority of the TBFC elves object, we don't have the time to go through so much network traffic! Sir Elfo chuckles, don't fret, for I have a powerful tool to assist us! I present to you RITA, Real Intelligence Threat Analytics. We just need to convert our PCAP file to Zeek logs, and RITA will do the rest! Anyone can do it, just follow today's tasks.

- ``` I have successfully started my target machine! ``` marks the completion of Task 1.

## Task 2 -> Detecting C2 with RITA
 ### RITA
  > Real Intelligence Threat Analytics (RITA) is an open-source framework created by Active Countermeasures. Its core functionality is to detect command and control (C2) communication by analyzing network traffic captures and logs.

Its primary features are:
- C2 beacon detection
- DNS tunneling detection
- Long connection detection
- Data exfiltration detection
- Checking threat intel feeds
- Score connections by severity
- Show the number of hosts communicating with a specific external IP
- Shows the datetime when the external host was first seen on the network

## Solution:
- The room says to convert ``` rita_challenge.pcap ``` into zeek_logs and using rita analyse it.
- Found rita_challenge.pcap in pcaps directory.
- Ran this command ``` zeek readpcap pcaps/rita_challenge.pcap zeek_logs/rita_challenge ```.
- Zeek logs got saved to ``` /home/ubuntu/zeek_logs/rita_challenge ```
- Then cding into it by ``` cd /home/ubuntu/zeek_logs/rita_challenge/ && ls ```, got all the zeek logs.
- Now imported this zeek log file into rita to analyze it using ``` rita import --logs ~/zeek_logs/rita_challenge/ --database ri_chall ```
- Now viewed that file using ``` rita view ri_chall ```
- Using rita analyzed that .pcap file according to the questions.

## Answers:
- ***How many hosts are communicating with malhare.net?***
  ```
  6
  ```
- ***Which Threat Modifier tells us the number of hosts communicating to a certain destination?***
  ```
  prevalence
  ```
- ***What is the highest number of connections to rabbithole.malhare.net?***
  ```
  40
  ```
- ***Which search filter would you use to search for all entries that communicate to rabbithole.malhare.net with a beacon score greater than 70% and sorted by connection duration (descending)?***
  ```
  dst:rabbithole.malhare.net beacon:>=70 sort:duration-desc
  ```
- ***Which port did the host 10.0.0.13 use to connect to rabbithole.malhare.net?***
  ```
  80
  ```
