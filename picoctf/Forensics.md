# Challenge 1: Trivial Flag Transfer Protocol
In the challenge, it is necesaary to find how the flag has been hidden.

## Flag:
```
picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}
```

## My Approach:
I was given with a capture file, so using ```Wire Shark``` I look for the meaningful files hidden in it and then exported them in the form of readable files into my machine. Files were named as:

```
1. instructions.txt
2. plan
3. program.deb
4. picture1.bmp
5. picture2.bmp
6. picture3.bmp
```

First two files had some gibberish text written in it so to decipher it I used ROT13 decoder and found there were some messages in it. First file contained  ```TFTP DOESNT ENCRYPT OUR TRAFFIC SO WE MUST DISGUISE OUR FLAGTRANSFER. FIGURE OUT A WAY TO HIDE THE FLAG AND I WILL CHECK BACK FOR THE PLAN``` and the second one contained ```I USED THE PROGRAM AND HID IT WITH-DUE DILIGENCE. CHECK OUT THE PHOTOS```. As the message says check out the photos, theyw were all bmp photos so I decided to check by manipulating their sizes, maybe I get the flag but it didn't worked. Then I thought there might be some link to this third file```program.deb```. So I read about it on google and found it's a debian file and it needs to be run at linux or any similar terminal. So, I used UBUNTU Terminal.
```
Microsoft Windows [Version 10.0.26200.6901]
(c) Microsoft Corporation. All rights reserved.

C:\Users\Krishna>wsl
krishna@ULTRON:/mnt/c/Users/Krishna$ sudo apt-get install ./program.deb
[sudo] password for krishna:
Reading package lists... Done
E: Unsupported file ./program.deb given on commandline
krishna@ULTRON:/mnt/c/Users/Krishna$ cd Downloads
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ sudo apt-get install ./program.deb
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Note, selecting 'steghide' instead of './program.deb'
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 steghide : Depends: libjpeg62-turbo (>= 1:1.3.1) but it is not installable
E: Unable to correct problems, you have held broken packages.
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ sudo apt install steghide
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
steghide is already the newest version (0.5.1-15).
0 upgraded, 0 newly installed, 0 to remove and 55 not upgraded.
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ steghide extract -sf ./picture1.bmp
Enter passphrase:
steghide: could not open the file "./picture1.bmp".
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ steghide extract -sf ./picture1.bmp -p "DUEDILIGENCE"
steghide: could not open the file "./picture1.bmp".
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ steghide extract -sf ./picture3.bmp -p "DUEDILIGENCE"
wrote extracted data to "flag.txt".
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ cat ./flag.txt
picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$
```

## My learnings:
Got to know about accessing and deciphering from capture files, then came to know about debiian files, how to extract data using stegnography using steghide.

## Wrong Tangets:
At start, I was not getting how to access .deb files on terminal, I was trying to access it in terminal but nothing worked then got to know about some sudo commands on google and then get the flag.



# Challenge 2: tunn3l v1s10n
In this challenge, a file is given and we have to recover the flag from it.

## Flag:
```
picoCTF{qu1t3_a_v13w_2020}
```

## My Approach:
As the type of file was not known, so it was necessary to know what type of file is it to start with it. I used ```HxD``` (a hex editor) to know about it's type. As I opened the file on hex editor, it showed a bulk of binary code alongside it's ASCII code. I watched on youtube how to read a file on hex editor, it said the first two bytes of the first line shows the type of the file and it showed ```42 4D```, then I searched what type of file's unicode it is, it said ```BITMAP```. So, now I know the type of the file, then I saved that hex file with a ```.bmp``` extension. Then I used ```GIMP (GNU Image Manipulation Program)``` to display the image in the saved file. In the image, it was written ```noflag{sorry}``` which means task was not done here. In the start, the video I watched also told about height and width of the image which is the next 4 bytes of the binary code ```first 2 for width and next 2 for height``` and by seeing the image, it was sure that height has to be changed. The image I got from hex editor shows it's size as ```1134x306```. So, definitely I had to increase the height of the image. I increased height to ```850 pixels``` by converting 850 into its equivalent hex ```0x352``` which in hexdump I had to change height from ```306=0x132``` to ```850=0x352```.

In the hexdump, 306 was displayed as ```32 01``` wwhich should be changed by ```52 03``` to increase height. Then I changed it and got an image with it's increased size and got the flag.

## My Learnings:
Got to learn about hex editors and how to manipulate files by manipulating their hex codes and to get to know about the type of an unknown file.

## Wrong Tangets:
In th video, I watched that the height and width are always the next 4 bytes of hex code after the type of file (file's format unicode), so  I was completely got focussed on the first line and was trying to manipulate the first line only blindly assuming that's the height and width code but I was wrong. Later I saw that the size of the image is given in the second line of the hexdump, as size says 1134x306, therefore it's hex code should be ```6E 04 32 10``` and then I changed the height and made hex code look like ```6E 04 52 03``` and then saved the image and got the flag.

# Challenge 3: m00nwalk
In the above challenge, an audio (.wav) file is given which depicts a message from moon. 

## Flag:
```
picoCTF{beep_boop_im_in_Space}
```

## My Approach:
After listening to the audio file from the moon and reading message that decode message from moon. I thought there would be an image or text hidden in the file. Then I went for given hints as it said ```How did pictures from the moon landing get sent back to Earth?``` I seaarched about it, I campe to know about Apollo 11 in which I got to know that SSTV is used to decode SSTV transmissions sent from moon. I searched for an SSTV decoder, ```https://sstv-decoder.mathieurenaud.fr/``` and uploaded that .wav file into it which gave me a picture which contains the above flag.

## My Learnings:
I learnt about how the pictures from moon are sent to earth, came to know about SSTV transmissions and got to know about tools to decode those transmissions.

## Wrong Tangents:
At start, I was not getting what to do, I was again again listening to the audio, opening it in Audacity and again listening to it. Then I tried to understand what hints actually means and searched about how pictures are actually sent from moon to earth and then I came to right track.
