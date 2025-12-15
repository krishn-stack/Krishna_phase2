# Database Reincursion:
   > First day as an intern at Citadel Corp and i'm already making strides!
Got rid of that bulky unnecessary security system and implemented my own simple solution.

## Flag: 
```
Didn't got
```

## Approach:
- As the challenge says that it got rid of bulky unnecessary security system and implemented own simple solution.
- I thought that those different types of filters have been removed so I tried using the SQL injection, I used earlier ``` ' OR '1'='1' -- ```, got to know that this injection is blocked,.
- After this, I tried with ``` AND ```, used ``` admin ``` and some more injection queries, nothing seems to work.
- I got to know that all of these queries have been blocked by the server.
- Used some normal queries like where 1=1 and some commenting queries but none of them worked.
- So, I used chatgpt to give me more of the queries to be used when these tautology queries are blocked, it gave me some with ``` null ```, I used them but none of them worked too.
- After trying for almost whole day, I gave up om that and moved to forensics.

## Concepts Learned:
- Got to know about some of the ``` null ``` SQL injection queries for bypass authentication.


# Ophelia's Truth 1:
  > A detective at Moscow PD, Department 19, receives a message asking him to check the forensic analysis portal for a DNA report. Attached to the message is a file containing a link to the portal. He opens the attachment, but initially, nothing seems to happen, so he overlooks it. Later, he realizes that a crucial file from an ongoing case has gone missing.
He has provided the forensic artifacts from his computer to you, his colleague at the cyber forensics department, to figure out what went wrong. Find:
> 1. The filename of the attachment
> 2. The ip from where the malware was executed
> 3. The CVE the attacker exploited.


## Flag:
```
Flag format: nite{file_name.ext_XXX.XXX.XXX.XXX_CVE-XXXX-XXXXX}
Didn't got the flag
```

## Approach:
- Downloaded the attachment, got an zipped fle, unzipped it using WINRAR.
- Got ``` ophelia.raw ``` named file after unzipping the zipped file so I got the first part of the challenge.
- Moved for finding the i.p address from this ``` .raw ``` file, I searched for how to get the i.p address from this .raw file, got to know that this challlenge is related to the ``` Memory Forensics ```.
- Decided to use Volatility, tried using it but nothing worked, I tried using different plugins after reading what it does but none of the plugins seems to be working.














