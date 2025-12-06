# AI in Security - old sAInt nick
 > Unleash the power of AI by exploring it's uses within cyber security.

## Task 1 -> Introduction:
  > The lights glimmer and servers hum blissfully at The Best Festival Company (TBFC), melting the snow surrounding the data centre. TBFC has continued its pursuit of AI excellence. After the past two years, they realise that Van Chatty, their in-house chatbot, wasn’t quite meeting their standards. 

  > Unfortunately for the elves at TBFC, they are also not immune to performance metrics. The elves aim to find ways of increasing their velocity; something to manage the tedious, distracting tasks, which allows the elves to do the real magic. 

  > TBFC, adventurous as ever, is trialling their brand new cyber security AI assistant, Van SolveIT, which is capable of helping the elves with all their defensive, offensive, and software needs. They decide to put this flashy technology to use as Christmas approaches, to identify, confirm, and resolve any potential vulnerabilities, before any nay-sayers can.

- ``` I have successfully started the AttackBox and the target machine! ``` marks the coompletion of Task 1.

## Task 2 -> AI for Cyber Security Showcase:
  ### The Boom of AI Assistants
  > Ah, yes, artificial intelligence, that buzzword that seems here to stay. Who would have thought? Today’s room will highlight some ways AI is utilised in cyber security, along with important considerations to bear in mind when deploying AI for such tasks.
Particularly at the time of writing, AI is increasingly seen as a tool to boost speed by handling often tedious, time-consuming tasks, allowing humans to perform the real magic. Organisations want to see experience, not avoidance, in how these tools are operated.
GPT this, GPT that, we’ve all heard it often. And it’s likely to persist. As AI’s capabilities expand daily, we’ve observed a shift from AI being just “something to ask because you were too lazy to Google” (a mistake I’ve made myself). Now, AI is being embedded into everyday workflows, transforming how tasks are done and boosting productivity like never before.

### Defensive Security
  > AI agents are being used in blue teaming to speed up detection, investigation, and response, making them quicker and more dependable. Acting like automated assistants, these agents continuously process telemetry (logs, network flows, endpoint signals) and add context to alerts. Furthermore, we are witnessing the integration of AI into vendor appliances—such as AI-assisted firewalling and intrusion detection systems.
Beyond just detecting threats, AI can also assist in automating responses. Picture your system automatically isolating an infected device, blocking a suspicious email, or flagging an unusual login attempt — all in real time.

### Offensive Security
  > AI agents have made a notable impact on offensive security by automating and handling the often very labourious and time-consuming tasks that a pentester might traditionally undertake. 
For example, AI can be a powerful tool in a penetration tester's workflow for reconnaissance and information gathering, from OSINT to analysing noisy scanner outputs and mapping attack surfaces. This allows the pentester to spend more time on the crucial tasks that require a human touch.

### Software
  > AI-driven software development, rightfully, sounds a bit frightening. Isn't that so? Well, you wouldn't be wrong to feel this way; we've all heard about the popularity of vibe coding and the vulnerabilities introduced by AI.
However, AI has proven to be a valuable addition to the software development process in several ways. One example is a virtual "colleague" to bounce ideas off while writing the code itself. More importantly, it is used as a SAST/DAST scanner. These scanners audit and analyse written code and applications for potential vulnerabilities.


## Answers and Flags:
```
THM{AI_MANIA}
THM{SQLI_EXPLOIT}
```

## Concepts Learned:
- How to use AI to help us solve any challenge by making it work to write us some code snippets.

## Solution:
- After starting ``` Attacker Box ``` and ``` Target Machine ```, opened this site http://MACHINE_IP.
- Started interacting with ``` Van SolveIT ``` AI chat box.
- It gave a code of ``` script.py ```.
- Saved it on terminal and made it run in the terminal after changing the machine I.P. address.
- Got ``` THM{SQLI_EXPLOIT} ```, this flag.

- After, I started to interact with the AI and at last got the other flag.




