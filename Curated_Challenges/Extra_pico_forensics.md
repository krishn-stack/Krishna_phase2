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
  - Event viewer.
 

# PcapPoisoning:
  > How about some hide and seek heh?
Download this file and find the flag.

## Flag:
```
picoCTF{P64P_4N4L7S1S_SU55355FUL_f621fa37}
```

## Approach:
- Opened  ``` trace.pcap ``` file on wireshark.
- Analysed the protocol packets and got the flag.

  <img width="1333" height="996" alt="Screenshot 2025-12-07 170435" src="https://github.com/user-attachments/assets/aab9d263-96c6-44e0-8026-dbffabe7ca61" />


# Mob psycho:
  > Can you handle APKs?

## Flag:
```
picoCTF{ax8mC0RU6ve_NX85l4ax8mCl_5e67ea5e}
```

## Approach:
- We were given with a ``` .apk ``` file.
- Took the hint and got to know that it needs to be unzipped.
- Searched how to unzip an .apk file, got to know by changing its extension from ``` .apk ``` to  ``` .zip ```.
- It can now be unzipped.
- Used Winrar to unzip it, got variouss folders inside that.
- Searched for ``` flag.txt ```, it has a huge hex format text  ``` 7069636f4354467b6178386d433052553676655f4e5838356c346178386d436c5f35653637656135657d ```.
- Went to https://cyberchef.org and decoded it and got the flag.

  ## Concepts Learned:
  - How to handle .apk files by unzipping it.
 

# MSB:
  > This image passes LSB statistical analysis, but we can't help but think there must be something to the visual artifacts present in this image...

## Flag:
```
picoCTF{15_y0ur_que57_qu1x071c_0r_h3r01c_b5e03bc5}
```

## Approach:
- Since the challenge asks for MSB, so I thought it must be asking for image's most significant bits(MSBs) of the RGB values which are the main cause of any images's resolution.
- Went to [https://stegonline](https://georgeom.net/StegOnline/upload) site and uploaded the ``` .png ``` file and then clixked on extract data.
- Selected the MSBs of RGB values of the image.
- Got an extract bunch of .txt document in which I searched for the flag.

## Concepts Learned:
- Learned about the RGB values of the image.
- How they can be used to extract hidden data.


# endianness-v2:
  > Here's a file that was recovered from a 32-bits system that organized the bytes a weird way. We're not even sure what type of file it is.

## Flag:
```
picoCTF{cert!f1Ed_iNd!4n_s0rrY_3nDian_76e05f49}
```

## Approach:
- The challenge given says that file is recovered from a 32-bit system and bytes are unorganised.
- So, firstly I searched for the file format as I knew that it is related to hexdump of the file.
- Using ``` exiftool ```, I got to know that it is a ``` JPEG ``` file and since it is from 32 bit system, it means that every 4 bytes has to be reversed and hence needed to be modified.
- I searched for a command if there any exists which can manipulate the whole hexdump at once and I don't need to do all of it manually and I got one.
- I used ``` hexdump -v -e '1/4 "%08x"' -e '"\n"' challengefile | xxd -r -p > output_file ``` command to reverse the complete hexdump and store it in a ``` output_file ```.
- Opened ``` output_file ``` using ``` GIMP ``` and got the flag.

## Concepts Learned:
- Got to know about the ``` little endian ``` and ``` big endian ``` format.
- Learned how to manipulate them using hexdump command.


# DISKO 2:
   > Can you find the flag in this disk image? The right one is Linux! One wrong step and its all gone!

## Flag;
```
picoCTF{4_P4Rt_1t_i5_a93c3ba0}
```

## Approach:
- Downloaded the file, got a zipped file.
- Extracted it using WINRAR appplication.
- Opened it HxD and using its ``` Find ``` utility seared for ``` picoCTF ```.
- At first, I searched from forward direction, i got a wrong one.
- Then I thought of searching from the backward direction, did that and got the flag from hexdump.




