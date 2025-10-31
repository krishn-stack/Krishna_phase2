# Challenge 1: rsa_oracle
The challenge is provided with a secret.enc file (ciphertext file) and an encrypted password.enc file, challenge asks us to deccrypt the password.enc file and get  the flag.

## Flag:
```
picoCTF{su((3ss_(r@ck1ng_r3@_da099d93}
```

## My Approach:
We have been given a secret.enc and password.enc file which contains a ciphered text of password to the secret.enc file and which needs to be decrypted. I dont't know much of the coding, so took help from chatgpt and from various sites to decipher that ciphered password as hint is given to chose chosen plaintext attack. While deciphering, I got ```0x6461303939``` as the hex code for ciphered text and its equivalent ASCII I got was ```da099```. Then I checked it in the oracle's encryption program, it gave the same ciphered text. So, it was the plaintext password for the file. 
Then I used the command given in the hint to decipher the secret.enc file using that password and got the flag.

## Command Used:
```
 openssl enc -aes-256-cbc -d -in secret.enc -k da099
```

## My Solve:
```
Microsoft Windows [Version 10.0.26200.7019]
(c) Microsoft Corporation. All rights reserved.

C:\Users\Krishna>wsl
krishna@ULTRON:/mnt/c/Users/Krishna$ nc titan.picoctf.net 50616
*****************************************
****************THE ORACLE***************
*****************************************
what should we do for you?
E --> encrypt D --> decrypt.
E
enter text to encrypt (encoded length must be less than keysize): e
e

encoded cleartext as Hex m: 65

ciphertext (m ^ e mod n) 2914164017270963930937868722466869408022807415973365004325338399211467601153124260350527660034792243795980989219063339385786999199686204275562956335980305

what should we do for you?
E --> encrypt D --> decrypt.
D
Enter text to decrypt: 2914164017270963930937868722466869408022807415973365004325338399211467601153124260350527660034792243795980989219063339385786999199686204275562956335980305
decrypted ciphertext as hex (c ^ d mod n): 65
decrypted ciphertext: e

what should we do for you?
E --> encrypt D --> decrypt.
E
enter text to encrypt (encoded length must be less than keysize): da099
da099

encoded cleartext as Hex m: 6461303939

ciphertext (m ^ e mod n) 4228273471152570993857755209040611143227336245190875847649142807501848960847851973658239485570030833999780269457000091948785164374915942471027917017922546

krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ openssl enc -aes-256-cbc -d -in secret.enc -p da099
enc: Use -help for summary.
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ -help
Command '-help' not found, did you mean:
  command 'dhelp' from deb dhelp (0.6.30)
Try: sudo apt install <deb name>
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ openssl enc -help
Usage: enc [options]

General options:
 -help               Display this summary
 -list               List ciphers
 -ciphers            Alias for -list
 -e                  Encrypt
 -d                  Decrypt
 -p                  Print the iv/key
 -P                  Print the iv/key and exit
 -engine val         Use engine, possibly a hardware device

Input options:
 -in infile          Input file
 -k val              Passphrase
 -kfile infile       Read passphrase from file

Output options:
 -out outfile        Output file
 -pass val           Passphrase source
 -v                  Verbose output
 -a                  Base64 encode/decode, depending on encryption flag
 -base64             Same as option -a
 -A                  Used with -[base64|a] to specify base64 buffer as a single line

Encryption options:
 -nopad              Disable standard block padding
 -salt               Use salt in the KDF (default)
 -nosalt             Do not use salt in the KDF
 -debug              Print debug info
 -bufsize val        Buffer size
 -K val              Raw key, in hex
 -S val              Salt, in hex
 -iv val             IV in hex
 -md val             Use specified digest to create a key from the passphrase
 -iter +int          Specify the iteration count and force the use of PBKDF2
                     Default: 10000
 -pbkdf2             Use password-based key derivation function 2 (PBKDF2)
                     Use -iter to change the iteration count from 10000
 -none               Don't encrypt
 -*                  Any supported cipher

Random state options:
 -rand val           Load the given file(s) into the random number generator
 -writerand outfile  Write random data to the specified file

Provider options:
 -provider-path val  Provider load path (must be before 'provider' argument if required)
 -provider val       Provider to load (can be specified multiple times)
 -propquery val      Property query used when fetching algorithms
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ openssl enc -aes-256-cbc -d -in secret.enc -k da099
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
picoCTF{su((3ss_(r@ck1ng_r3@_da099d93}krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$
```

## My Learnings:
Got to know about cryptography model chosen plaintext attack and tried to make code to decrypt ciphered password but were not able to so had to take help from chatgpt and other websites.  


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


# Challenge 3: miniRSA
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
