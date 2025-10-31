# Challenge 1: IQ Test:
The challenge is provided with a 36 bit input logic gate diagram with a sample input.

## Flag:
```
nite{100010011000}
```

## My Approach:
I  made a copy of the diagram on some sheets and tried solving for those gates and got the flag:
<img width="920" height="1518" alt="image" src="https://github.com/user-attachments/assets/fdb4e29c-5e9d-4cdb-af01-7e2ad5fb6957" />


## My Learnings:
Got to learn to deal with these types of complex logic gates and finding output.

## Wrong Tangets:
At  first I took x<sub>0</sub> as the last bit and tried solving that which gave me the wrong output as well as the wrong flag.


# Challenge 2: I like Logic:
The challenge is given with a challenge.sal file in which it has many .bin and one json files. We need to find what common in all of those.

## Flag:
```
FCSC{b1dee4eeadf6c4e60aeb142b0b486344e64b12b40d1046de95c89ba5e23a9925}
```
## My Approach:
First I searched about what is a .sal file and what to do with it, how to extract information from it. I got to know about a software called ```Logic 2``` software which I used to analyse that ```challenge.sal``` file. Basically, I got to know that .sal file is a capture file used for debugging hardware and doing analysis and a software needed to do it. I opened that file in that software, setup the analyzer named ```Async Serial``` in that I set input channel as ```Channel 3``` and saved it. I got a table along with a terminal version of it. I switched to terminal version and found a bunch of english paragraphs. While I was scrolling it, I got the flag in between those paragraphs.

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/c141aa0c-468b-4c35-8779-c18c5f70d60e" />
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/26c85622-6f0a-48b4-9826-4213cb6ba811" />


## My  Learning:
Got to  learn about .sal file and a software to analyse .sal files.

## Wrong Tangets:
At first, I didn't saw there's a challenge.sal file, I simply opened it and looked for those .bin files and was trying to do things with them.


