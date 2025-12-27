# CyberChef - Hoperation Save McSkidy
  > The story continues, and the elves mount a rescue and will try to breach the Quantum Fortress's defenses and free McSkidy.

## Task 1 -> Introduction
 > McSkidy is imprisoned in King Malhare's Quantum Warren. Sir BreachBlocker III was put in charge of securing the fortress and implemented several access controls to prevent any escape. His defenses are worthy of his name.

> However, McSkidy managed to send vital clues to his team using harmless bunny pictures. One message revealed that five locks needed to be disabled to secure an escape route. The locks can be broken by examining their logic and leveraging the system's built-in chat for the guards. They can be eluded in revealing vital details or even passwords. However, you will need to speak their language.

- ``` Let us siege the fortress! ``` marks the completion of Task 1.

## Task 2 -> Important Concepts
 ### Encoding and Decoding
  ```
  Encoding is a method to transform data to ensure compatibility between different systems. It differs from encryption in purpose and process.
  ```

  <img width="907" height="503" alt="image" src="https://github.com/user-attachments/assets/2a2fe226-5e13-4c86-a00c-a5ed4c560cd0" />

  ```
  Decoding is the process of converting encoded data back to its original, readable, and usable form.
  ```

### Inspecting Web Pages
 > Besides the rendered content of a web page, your browser usually receives and can show additional information.
- By opening ``` Developer Tools ``` and inspecting can show many things which your browser doesn't render on the webpage.

- ``` Locked and loaded. ``` marks the completion of Task 2.

## Task 3 -> First Lock - Outer Gate
 > McSkidy revealed some vital clues in his message. You will have to leverage any useful piece of information in order to break the locks.

***Key points to look out for:*** 
- Chat is Base64 encoded
- Guard name
- Headers
- Login Logic

### Solution
- Opened site using ``` http://MACHINE_IP:8080 ```
- In the chatbox, Guard Name -> ``` CottonTail ```, encoded it into Base64 format and got ``` Q290dG9uVGFpbA== ```
- Opened Inspect -> Network, there was given ***X-Magic Question:*** What is the password for this level?
- Opened Debugger and checked the Login Logic for knowing how to get the password.
- It said ``` From Base64 ```, so I encoded this question in the Base64 format and sent it to the chatbox.
- It gave a base64 encoded text, decoded it and got the password.

  ## Answers:
  ***What is the password for the first lock?***
  ```
  Iamsofluffy
  ```

## Task 4 -> Second Lock - Outer Wall
> Excellent job breaking that first level.
This level nudges the difficulty up a little bit, but don’t worry, you will figure it out. Let’s go!

### Solution:
- Again got the Guard name -> ``` CarrotHelm ``` , encoded it and got ``` Q2Fycm90SGVsbQ== ```
- Opened Network in the Inspect view, got another question -> ``` Did you change the password? ```
- Encoded it and sent it to the chatbox, it gave a base64 text.
- Decoded it twice and got the password.

## Answers:
***What is the password for the second lock?***
```
Itoldyoutochangeit!
```

## Task 5 -> Third Lock - Guard House
 > So far, so good. As you saw in the previous level, the login logic begins to use chained operations.

### Solutions:
- Got another Guard name -> ``` LongEars ```, encoded it and got ``` TG9uZ0VhcnM= ```
- Opened Network in the Inspect view, and got ***X-Recipe Key:*** cyberchef.
- Asked the chatbox to give me the password in a polite way after encoding it into base64 format aas it understands only that.
- It gave a base64 text.
- Checked for the Login Logic, it said ``` From Base64 => XOR ```.
- Used CyberChef and decoded the text given by chatbox and xored it and got the password.

## Answers:
***What is the password for the third lock?***
```
BugsBunny
```

## Task 6 -> Fourth Lock - Inner Castle
 > We are almost there. In this level, Sir BreachBlocker III throws you a curveball. Let’s see how to tackle this.

### Solution:
- Got another Guard name -> ``` Lenny ```, encoded it and got ``` TGVubnk= ```
- Got ``` hash lookup ``` in the Login Logic.
- Again asked for the password politely from the chatbox, it gave a base64 text.
- Decoded it, got a hashed password.
- Opened an online free hash cracker, entered the hashed password, and got plaintext password.

## Answer:
***What is the password for the fourth lock?***
```
passw0rd1
```

## Task 7 -> Fifth Lock - Prison Tower
 > Ready for the final hurdle?

> As the defenses weaken, you receive another hidden message from McSkidy:

> “I can see you are ready to break the last lock. Be aware that Sir BreachBlocker III implemented different mechanisms for the last lock, which change occasionally. Make sure you match the correct approach when decoding the password.”

> That sounds tricky, but do not despair. You will find a way.

### Solution:
- Got another Guard name -> ``` Carl ```, encoded it and got ``` Q2FybA== ```
- Opened Network and got ***X-Recipe Key:*** cyberchef along with ***X-Recipe ID:*** R1.
- Checked the Logic Logic, it said for R1 -> ``` From Base64 ⇒ Reverse ⇒ ROT13 ```
- Again asked for the password politely from the chatbox, it gave encoded text.
- Decoded this text from Base64, then revered the decoded output and then at last did ROT 13 and got the answer.

  ## Answers:
-  ***What is the password for the fifth lock?***
   ```
   51rBr34chBl0ck3r
   ```
- ***What is the retrieved flag?***
  ```
  THM{M3D13V4L_D3C0D3R_4D3P7}
  ```
    




















 
