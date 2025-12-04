# Splunk Basics - Did you SIEM?
  > Learn how to ingest and parse custom log data using Splunk.

## Task 1 -> Introduction:
  > It’s almost Christmas in Wareville, and the team of The Best Festival Company (TBFC) is busy preparing for the big celebration. Everything is running smoothly until the SOC dashboard flashes red. A ransom message suddenly appears:

  <img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/10b0e8a8-cbca-44e3-b7bd-48a96acdf4d5" />

  > The message comes from King Malhare, the jealous ruler of HopSec Island, who’s tired of Easter being forgotten. He’s sent his Bandit Bunnies to attack TBFC’s systems and turn Christmas into his new holiday, EAST-mas.

  > With McSkidy missing and the network under attack, the TBFC SOC team will utilize Splunk to determine how the ransomware infiltrated the system and prevent King Malhare’s plan from being compromised before Christmas.

- ```  I successfully have access to the Splunk instance!  ```  marks the completion of Task 1.

## Task 2 -> Log Analysis with Splunk:
  > Exploring the Logs
  > In the Splunk instance, the data has been pre-ingested for us to investigate the incident.

## Answers:
- What is the attacker IP found attacking and compromising the web server?
  > 198.51.100.55
- Which day was the peak traffic in the logs? (Format: YYYY-MM-DD)
  > 2025-10-12
- What is the count of Havij user_agent events found in the logs?
  > 993
- How many path traversal attempts to access sensitive files on the server were observed?
  > 658
- Examine the firewall logs. How many bytes were transferred to the C2 server IP from the compromised web server?
  > 126167

## Solution:
- click on ``` Search & Reporting ```
- type query ``` index = main ``` and check 2 sourcetype: ``` web_traffic ``` and ``` firewall_logs ```

# Queries used:
- ## Initial Triage
  > index=main sourcetype=web_traffic
- ## Visualizing the Logs Timeline
  > index=main sourcetype=web_traffic | timechart span=1d count
  > index=main sourcetype=web_traffic | timechart span=1d count | sort by count | reverse
- ## Filtering out Benign Values
  > index=main sourcetype=web_traffic user_agent!=*Mozilla* user_agent!=*Chrome* user_agent!=*Safari* user_agent!=*Firefox*
- ## Narrowing Down Suspicious IPs
  > index=main sourcetype=web_traffic user_agent!=*Mozilla* user_agent!=*Chrome* user_agent!=*Safari* user_agent!=*Firefox* | stats count by client_ip | sort -count | head 5
- ## Tracing the Attack Chain
  > index=main sourcetype=web_traffic client_ip="<REDACTED>" AND path IN ("/.env", "/*phpinfo*", "/.git*") | table _time, path, user_agent, status
- ## Enumeration (Vulnerability Testing)
  > index=main sourcetype=web_traffic client_ip="<REDACTED>" AND path="*..*" OR path="*redirect*"
  > index=main sourcetype=web_traffic client_ip="<REDACTED>" AND path="*..\/..\/*" OR path="*redirect*" | stats count by path
- ## SQL Injection Attack
  > index=main sourcetype=web_traffic client_ip="<REDACTED>" AND user_agent IN ("*sqlmap*", "*Havij*") | table _time, path, status
- ## Exfiltration Attempts
  > index=main sourcetype=web_traffic client_ip="<REDACTED>" AND path IN ("*backup.zip*", "*logs.tar.gz*") | table _time path, user_agent
- ## Ransomware Staging & RCE
  > index=main sourcetype=web_traffic client_ip="<REDACTED>" AND path IN ("*bunnylock.bin*", "*shell.php?cmd=*") | table _time, path, user_agent, status
- ## Correlate Outbound C2 Communication
  > index=main sourcetype=firewall_logs src_ip="10.10.1.5" AND dest_ip="<REDACTED>" AND action="ALLOWED" | table _time, action, protocol, src_ip, dest_ip, dest_port, reason
- ## Volume of Data Exfiltrated
  > index=main sourcetype=firewall_logs src_ip="10.10.1.5" AND dest_ip="<REDACTED>" AND action="ALLOWED" | stats sum(bytes_transferred) by src_ip


## Concepts Learned:
- Splunk



















