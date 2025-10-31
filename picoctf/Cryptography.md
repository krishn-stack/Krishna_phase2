# Challenge 2: Custom encryption
The challenge is given with an encryption code and asks to develop a decryption model to decrypt the cipher into plain text.

## Flag:
```
picoCTF{custom_d2cr0pt6d_49fbee5b}
```

## My Approach:
As the challenge says to get the sense of the encryption code given, I look over that python code to understand what going on. For that, I saw the code and took help from chatgpt to some extent (not gonna lie) to understand what the code is actually about and also to get help in getting the decryption code. After that I run on the inputs given and got the flag.

## My Learnings:
Got to know about chosen plain-text attack in cryptography and tried to build a decryption model for the given encryption model (ofcourse I didn't make it on my own, I had to take help from chatgpt).


## Challenge 3: miniRSA
The challenge is given by a ciphertext file which needs to be deecrypted using information in that file.

```
picoCTF{n33d_a_lArg3r_e_ccaa7776}
```

## My Approach:
As the hints mentioned says to check for RSA, after seeing it's tutorial I knew that this ciphertext is to be decoded using that N and e.
While scrolling, I got a website called ```dCode```, a RSA ciphertext decoder, it asks for all the 3 given things, I put it there and got the flag.


## My Learnings:
Got to know about RSA (Rivest–Shamir–Adleman) cryptosystem which needs a private/public key to decipher a plaintext message and got to know about it's decoder website named ```dCode```

## Site Link:
```
https://www.dcode.fr/rsa-cipher
```
