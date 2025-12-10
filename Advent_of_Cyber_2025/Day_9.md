# Passwords - A Cracking Christmas
   > Learn how to crack password-based encrypted files.

## Task 1 -> Introduction
  > With time between Easter and Christmas being destabilised, the once-quiet systems of The Best Festival Company began showing traces of encrypted data buried deep within their servers. Sir Carrotbane, stumbled upon a series of locked PDF and ZIP files labelled “North Pole Asset List.” Rumours spread that these could contain fragments of Santa’s master gift registry, critical information that could help Malhare control the festive balance between both worlds.
Sir Carrotbane sets out to crack the encryption, learning how weak passwords can expose even the most guarded secrets. Can the Elves adapt fast and prevent their secrets from being discovered?

- ``` I have successfully started the target machine in split view, or connected via the THM VPN and SSH! ``` marks the completion of Task 1.

## Task 2 -> Attacks Against Encrypted Files
  > Attackers don't usually try to "break" the encryption itself because that would take far too long with modern cryptography. Instead, they focus on guessing the password that protects the file. The two most common ways of doing this are dictionary attacks and brute-force (or mask) attacks.

### Dictionary Attacks
  > In a dictionary attack, the attacker uses a predefined list of potential passwords, known as a wordlist, and tests each one until the correct password is found. These wordlists often contain leaked passwords from previous breaches, common substitutions like password123, predictable combinations of names and dates, and other patterns that people frequently use. Because many users choose weak or common passwords, dictionary attacks are usually fast and highly effective.

### Mask Attacks
  > Brute-force and mask attacks go one step further. A brute-force attack systematically tries every possible combination of characters until it finds the right one. While this guarantees success eventually, the time it takes grows exponentially with the length and complexity of the password.

  > Mask attacks aim to reduce that time by limiting guesses to a specific format. For example, trying all combinations of three lowercase letters followed by two digits.

### Practical tips attackers use :
- Start with a wordlist (fast wins). Common lists: ``` rockyou.txt ```, ``` common-passwords.txt ```.
- If the wordlist fails, move to targeted wordlists (company names, project names, or data from the target).
- If that fails, try mask or incremental attacks on short passwords (e.g. ``` ?l?l?l?d?d ``` = three lowercase letters + two digits, which is used as a password mask format by password cracking tools).
- Use GPU-accelerated cracking when possible; it dramatically speeds up attacks for some algorithms.
- Keep an eye on resource use: cracking is CPU/GPU intensive. That behaviour can be detected on a monitored endpoint.

## Flags:
```
THM{Cr4ck1ng_PDFs_1s_34$y}
THM{Cr4ck1n6_z1p$_1s_34$yyyy}
```

## Concepts Learned:
- Revised how to find passwords for protected files using wordlists like ``` rockyou.txt ```.

## Solution:
- The challenge is provided with 2 files: ``` flag.pdf ``` and ``` flag.zip ```.
- The passwords for both the files need to be found using some specific commands and wordlists.
  

### Tools to Use:
1. PDF: ``` pdfcrack ```, ``` john ```(via ``` pdf2john ```)
2. ZIP: ``` fcrackzip ```,``` john ```(via ``` zip2john ```)
3. General: ``` john ``` (very flexible) and ``` hashcat ``` (GPU acceleration, more advanced)


- Starting with pdf, I used this command ``` pdfcrack -f flag.pdf -w /usr/share/wordlists/rockyou.txt ``` and got the password for pdf file as ``` naughtylist ```.
- Next moving on to ``` flag.zip ``` file, used this command ``` zip2john flag.zip > ziphash.txt ```, this command creates a hash that ``` john ``` can understand amd then used this ``` john --wordlist=/usr/share/wordlists/rockyou.txt ziphash.txt ``` and got the password as ``` winter4ever ```.
- After that, simply opened both of the files using these 2 passwords on respective files and got both the flags.
