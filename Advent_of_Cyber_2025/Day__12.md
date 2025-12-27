# Phishing - Phishmas Greetings
  > Learn how to spot phishing emails from Malhare's Eggsploit Bunnies sent to TBFC users.

## Task 1 -> Introduction
  > Since McSkidy’s disappearance, TBFC’s defences have weakened, and now the Email Protection Platform is down.
With filters offline, the staff must triage every suspicious message manually.
The SOC Team suspects Malhare’s Eggsploit Bunnies have sent phishing messages to TBFC’s users to steal credentials and disrupt SOC-mas.

> You’ve joined the Incident Response Task Force to help identify which emails are legit or phishing attempts.
But beware, some phishing attempts are clever, disguised as routine TBFC operations, volunteer sign-ups, or SOC-mas event logistics. Every wrong call could bring Wareville one step closer to EAST-mas becoming a reality.

- ``` I have access to the Wareville Email Threat Inspector!  ``` marks the completion of Task 1.

## Task 2 -> Spotting Phishing Emails
  ### Phishing
   > Phishing may be one of the oldest cyber tricks, but it’s still one of the most effective. As companies like TBFC strengthen their defences with advanced email filters and security tools, attackers have evolved their tactics to stay one step ahead.

> Common intentions behind phishing messages:
> 1. Credential theft: Tricking users into revealing passwords or login details.
> 2. Malware delivery: Disguising malicious attachments or links as safe content.
> 3. Data exfiltration: Gathering sensitive company or personal information.
> 4. Financial fraud: Persuading victims to transfer money or approve fake invoices.

### Spam
 > Spam is just digital noise: annoying, but mostly harmless. Phishing, however, is a precision strike, in this case from Malhare’s Eggsploit Bunnies, crafted to deceive TBFC employees and open a path into the company’s defences.
Spam focuses on quantity over precision. Unlike phishing, which aims to deceive specific users, spam messages are sent in bulk to flood inboxes with unwanted marketing or irrelevant content. Their goal isn’t usually to steal data, but to push exposure or engagement.

> Common intentions behind spam messages:
> 1. Promotion: Advertising products, services, or events. Often unsolicited or low-quality.
> 2. Scams: Spreading fake offers or “get rich quick” schemes to attract clicks.
> 3. Traffic generation (clickbait): Driving users to external sites or boosting ad metrics.
> 4. Data harvesting: Collecting active email addresses for future campaigns.

***Attacker often use some of the following techniques for phishing several users:***
1. Impersonation
2. Social Engineering
3. Typosquatting and Punnycode
4. Spoofing
5. Malicious Attachments

### Impersontaion
  > Some attackers may act as a person, department, or even a service to lure users. This is a way to gain credibility by impersonating the recipient manager or an important person within the company.

***For example***: Instead of email address ``` krishna@tbfc.com ```
```
krishna@gmail.com
```

### Social Engineering
 > Social engineering in phishing is the art of manipulating people rather than breaking technology. Attackers craft believable stories, emails, calls, or chat messages that exploit emotions (fear, helpfulness, curiosity, urgency) and real-world context to lure the recipients of a message.

- In this type of technique, attacker plays with the emotions of people and manipulate them to do what attacker wants them to do. If any mail is manipulating with some urgent work, making you feel emotional then this could be considered as ***Social Engineering*** technique.


### Typosquatting and Punnycode
  > Typosquatting is when an attacker registers a common misspelling of an organisation's domain. For example, glthub.com instead of github.com (note that there is an L instead of an i).

   <img width="888" height="452" alt="image" src="https://github.com/user-attachments/assets/df22b1a2-3f29-472e-bf5f-39b0b8e923f2" />

  > Punycode is a special encoding system that converts Unicode characters (used in writing systems like Chinese, Cyrillic, and Arabic) into ASCII. When typing punycodes in the browser URL bar, this will be translated into ASCII format, which is the accepted format by DNS.

 ***For example:***
 - ``` a ``` changed with ``` α ```
 - ``` r ``` changed with ``` г ```

   <img width="632" height="375" alt="image" src="https://github.com/user-attachments/assets/50d5845c-b858-4b08-827c-1bd36603cddb" />

### Spoofing
  > Email spoofing is another way attackers can trick users into thinking they are receiving emails from a legitimate domain.
The message looks like it came from a trusted sender (the display name and “From:” you see in the preview), but the underlying headers tell a different story.

- So, to check for spoofing, let's analyse ***Headers:*** ``` Authentication-Results ``` and ``` Return-Path ```
- In Authentication-Results, if ``` spf ``` and ``` dmarc ``` both fails, it's a strong sign of spoofing.
- If Return-Path doesn't match with the sender address, it means it's definitely a spoofing.

### Malicious Attachments
 > The most classic way of phishing is attaching malicious files to an email. Usually, these attachments are sent using some sort of social engineering technique in the body.

## Solution:
- The room is given with a Inbox link of the TBFC
  ```
  https://LAB_WEB_URL.p.thmlabs.com.
  ```
- Analysed each emails in the inbox.
- Figuered out which email is Phishing mail and which email is just a spam.
- If it's a Phishing mail then what types of techniques are used in that mail, selected those techniques and got the flags for each mail.

## Flags:
```
THM{yougotnumber1-keep-it-going}
THM{nmumber2-was-not-tha-thard!}
THM{Impersonation-is-areal-thing-keepIt}
THM{Get-back-SOC-mas!!}
THM{It-was-just-a-sp4m!!}
THM{number6-is-the-last-one!-DX!}
```
























