# Challenge 3: m00nwalk
In the above challenge, an audio (.wav) file is given which depicts a message from moon. 

## Flag:
```
picoCTF{beep_boop_im_in_Space}
```

## My Approach:
After listening to the audio file from the moon and reading message that decode message from moon. I thought there would be an image or text hidden in the file. Then I went for given hints as it said ```How did pictures from the moon landing get sent back to Earth?``` I seaarched about it, I campe to know about Apollo 11 in which I got to know that SSTV is used to decode SSTV transmissions sent from moon. I searched for an SSTV deecoder, ```https://sstv-decoder.mathieurenaud.fr/``` and uploaded that .wav file into it which gave me a picture which contains the above flag.

## My Learnings:
I learnt about how the pictures from moon are sent to earth, came to know about SSTV transmissions and got to know about tools to decode those transmissions.

## Wrong Tangents:
At start, I was not getting what to do, I was again again listening to the audio, opening it in Audacity and again listening to it. Then I tried to understand what hints actually means and searched about how pictures are actually sent from moon to earth and then I came to right track.
