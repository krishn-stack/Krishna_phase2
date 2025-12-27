# Obfuscation - The Egg Shell File
 > McSkidy keeps her focus on a particular alert that caught her interest: an email posing as northpole-hr.

## Task 1 -> Introduction
 > WareVille has not felt right since the wormhole appeared. Everyone in TBFC is on high alert: Systems are going haywire, dashboards are spiking, and SOC alerts have been firing nonstop. Amid the chaos, McSkidy keeps her focus on a particular alert that caught her interest: an email posing as northpole-hr. It’s littered with carrot emojis, but the weird thing is this: there is no North Pole human resources department. TBFC’s HR is at the South Pole.

> Digging further she found a tiny PowerShell file from that email was downloaded. Among the code are random strings of characters, all gibberish, nothing readable at a glance.

> McSkidy knows malicious actors often hide code and data using a technique called obfuscation. But what is it, really? And how can we decipher it?

- ``` Start the target machine and continue with the next task. ``` marks the completion of Task 1.

## Task 2 -> Obfuscation & Deobfuscation
 ```
 Obfuscation is the practice of making data hard to read and analyze. Attackers use it to evade basic detection and delay investigations.
 ```

 ### Solution:
 - Opened ``` SantaStealer.ps1 ``` and in it asked for two Deobfuscate.
 - In the first one, a base64 encoded text was given and it asked to decode it, decoded it and got an url pasted it where asked and ran the SantaStealer.ps1 file on the ``` Windows Powershell ``` terminal, got the first flag.
 - In the second one, it asked to deobfuscate using first XORing the ``` CANDY-CANE-API-KEY ``` using a single byte key ``` 0x37 ``` and then convert the output to the hexadecimal and paste that where asked.
 - Again ran the file in Powershell terminal and got second flag.


## Flags:
```
THM{C2_De0bfuscation_29838}
THM{API_Obfusc4tion_ftw_0283}
```
