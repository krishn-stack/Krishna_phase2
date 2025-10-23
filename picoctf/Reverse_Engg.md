## Challenge 1: GDB Baby 1

In this challenge, you have to use a disassembler tool (in my case, I used IDAFree-9.2) to disassemble a debugger0_a file given in the challennge.

## Flag:
```
picoCTF{549698}
```
## My Approach:
After done with the videos given in the resources section, I downloaded IDA disassembler and disassemble the given file in the challenge. Then I searched for the ```eax``` register at the end of the ```main```. On disassembling file, a graph overview file opened and I found a hex code beside the eax register: ```86342```, I converted it into decimal base system as said in the challenge. On converting, I got ```549698``` as decimal number which came out to be the flag for the challenge.

## New Learnings:
Through this challenge, I learnt how to use a disassembler and and how to debugg an assembly file.

## Wrong Tangets I got:
At start, I was opeing everything in the eax register and trying to use them as flag. When nothing worked, my focus went to the code written beside ```eax``` register and I noticedd their is a h letter mentioned after that. So I got to know that it's a hex code and then I converted it and got the answer. Inshort, I didn't noticed that h after that code.
