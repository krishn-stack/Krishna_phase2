# Phishing - Merry Clickmas:
 > Learn how to use the Social-Engineer Toolkit to send phishing emails.

## Answers and Flags:
- ```  unranked-wisdom-anthem  ```
- ```  1984000  ```

## Task 1 -> Introduction:
 > In light of several recent cyber security threats against The Best Festival Company (TBFC), the local red team has scheduled several penetration tests. The red   teamers proceeded to carry out a regular penetration test against their TBFC. Part of this exercise is to ensure that the employees are diligent when clicking links and that the company is well protected against the latest phishing attacks. This type of authorised phishing is a proven way to learn whether the cyber security awareness training has fruited.

> In this task, you will be part of the TBFC local red team with the elves Recon McRed, Exploit McRed, and Pivot McRed. You will help them plan and execute their phishing campaign. It is time to see if more cyber security awareness training is required.

- ```  I have successfully started the AttackBox and the target machine!  ``` marks the completion of Task 1.

## Task 2 -> Phishing Exercise for TBFC:
  > Social Engineering
  > Social engineering refers to manipulating a user to make a mistake. Examples of such mistakes include sharing a password, opening a malicious file, and approving a payment. The term “social” means that the target of such an attack is human beings, not computer systems. Consequently, the attacker relies on psychological tricks to get the target user to cooperate. Some psychological factors that can play a key role in the success of such attacks are urgency, curiosity, and authority. This is why some would refer to social engineering as “human hacking”.
  > Phishing
  > Phishing is a subset of social engineering in which the communication medium is mostly messages. At one point, the most common phishing attacks happened via email; however, the spread of smartphones, along with ubiquitous Internet access, has spread phishing to short text messages (smishing), voice calls (vishing), QR codes (quishing), and social-media direct messages. The attacker’s purpose is to make the target user click, open, or reply to a message so that the attacker can steal information, money, or access.

  > Unfortunately, phishing attacks are becoming harder to spot. Even careful people might fall target to such attacks if they don’t exercise proper care. TBFC cyber security awareness training teaches users about two anti-phishing mnemonics written as S.T.O.P. The first S.T.O.P. is from All Things Secured, which tells users to ask the following questions before acting on an email:

  > Suspicious?
  > Telling me to click something?
  > Offering me an amazing deal?
  > Pushing me to do something now?
  > The second S.T.O.P. reminds users to follow the following instructions:

  > Slow down. Scammers run on your adrenaline.
  > Type the address yourself. Don’t use the message’s link.
  > Open nothing unexpected. Verify first.
  > Prove the sender. Check the real From address/number, not just the display name.
  > After hours of periodic cyber security training, the red team checks to see if the TBFC staff can dodge “fishy” emails.

  > Building the Trap
  > You must sound very convincing as a penetration tester for a successful phishing attack. It’s not only how you write the phishing email or messages, but also how you set up the trap for the target. The trap can be anything, depending on your objectives and the research you conduct on the target. Sometimes, attackers aim to compromise the target’s machine, and they achieve this by attaching a malicious file to their phishing email. Attackers sometimes craft a web page that mimics a legitimate login page to steal the target’s credentials.

  > In this task, we aim to acquire the target user’s login credentials. Our trap would be a fake TBFC portal login page, which we attach to the phishing email and send to the target. But a login page itself is not enough. We need to host it and implement some logic to capture the credentials entered by the target. To facilitate your task, we have already set up a script that, when run, will host a fake login page. The phoney login page we created will capture all the credentials entered into the page.
