# Event-Viewing:
  > One of the employees at your company has their computer infected by malware! Turns out every time they try to switch on the computer, it shuts down right after they log in. The story given by the employee is as follows:
They installed software using an installer they downloaded online
They ran the installed software but it seemed to do nothing
Now every time they bootup and login to their computer, a black command prompt screen quickly opens and closes and their computer shuts down instantly.

## Flag:
```
picoCTF{Ev3nt_vi3wv3r_1s_a_pr3tty_us3ful_t00l_81ba3fe9}
```

## Approach:
- As the challenge is given with 3 storylines, following it challenge needs us to find these 3 logs -> ``` Installation ```, ``` Modified Registry ```, ``` Shutdown ```.
- Analyzed and got these logs on these ``` Event_id ```
  
     1. Installation -> 1033
 
        <img width="1918" height="1198" alt="image" src="https://github.com/user-attachments/assets/46053597-f50f-4a26-a059-221ec01d1bbd" />

     3. Registry Modifies -> 4657

        <img width="1918" height="1198" alt="image" src="https://github.com/user-attachments/assets/f1325e86-799a-4bd5-a997-6cf6b00de06a" />

     4. Shutdown -> 1074

        <img width="1918" height="1198" alt="image" src="https://github.com/user-attachments/assets/686548c6-5a30-420d-bd3f-262125e29024" />

- All these ids had some base64 coded text, encoded them one by one.
- Got the Flag.

  ## Concepts Learned:
  - Learned about how to view and analyze logs.
  - Event viwer
