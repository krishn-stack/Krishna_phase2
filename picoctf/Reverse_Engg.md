# Challenge 1: GDB Baby 1

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


# Chalenge 2: ARMssembly 1

In this challenge, there's a file given named ```chall_1.S``` in which you have to check for which argument code will print ```win``` as output.

## Flag:
```
picoCTF{00000d2a}
```

## My Approach:
After seeing the videos from the given resources in which a challenge ```ARMssembly 0``` challenge was solved and he explained about things how to know about things written in that challenge file. I applied that in the above challenge and found that when function ```func``` gets an argument as ```0```, result will be printed as ```win```.
I also checked given Hint too which says shift. I started to look over the file, I came up with an expression ```(79<<7)/3``` and this has to be the argument.
On solving it, ```(79*(2^7))/3 = 3370```. So after converting it to hex code using python terminal, ```hex(3370)```, I got hex code as ```0xd2a``` so as the challenge says no 0x and 32bits therefore, I put 5 zeros before d2a and by this I got the flag for the challenge.

## New Learnings:
Through this challenge, I get to know about how to know some things about assembly language and how to interpret what function in it is doing.

## Wrong Tangents:
I would not say them as wrong directions but yeah I didn't get this expression on my first attempt, I tried deriving expression 5 times and at 6th time I got it.


