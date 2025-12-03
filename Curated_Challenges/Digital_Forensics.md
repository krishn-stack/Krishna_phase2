# 1. HIDE and SEEK:
Sakamoto’s at it again with a game of hide and seek, but this time, it’s not with Shin or his daughter. An old friend hid some secret data in this image. Can you find it before the others do?

Hint: Even in retirement, Sakamoto never loses at hide and seek. Maybe stegseek can help you keep up.

## Flag:
```
nite{h1d3_4nd_s33k_but_w1th_st3g_sdfu9s8}
```
## Approach:

```
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ stegseek -sf sakamoto.jpg -wl rockyou.txt
StegSeek 0.6 - https://github.com/RickdeJager/StegSeek

[i] Found passphrase: "iloveyou1"
[i] Original filename: "flag.txt".
[i] Extracting to "sakamoto.jpg.out".

krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ cat flag.txt
���6�>��:=����␦1�0���=������<␦�2���09����7�4���3������2�6���65����=�8��K9������8�:��m<1����3�<��������>�>��12=����␦9�0���5������4�2���89����?4���;������:�6���>␦5����5�8��[1�����0�:��}41����;�<��������6�>��Q:=����␦1�0���=������<␦�2�
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ steghide extract -sf sakamoto.jpg
Enter passphrase:
the file "flag.txt" does already exist. overwrite ? (y/n) y
wrote extracted data to "flag.txt".
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ cat flag.txt
nite{h1d3_4nd_s33k_but_w1th_st3g_sdfu9s8}
```

## Concepts Learned:
- Learned to use stegseek
- Got to know about wordlist ```rockyou.txt```.




# 2.  Nutrela Chunks:
One of my favorite foods is soya chunks. But as I was enjoying some Nutrela today, I noticed a few chunks weren’t quite right. Seems like something’s off with their structure. Could you help me fix these broken chunks so I can enjoy my meal again?

## FLag:
```
nite{n0w_y0u_kn0w_ab0ut_PNG_chunk5}
```

## Approach:
- Opened corrupted PNG File in the HxD.
- Checked for correct PNG hexdump, hexdump for the given PNG file was wrong.
- Corrected it by editing ```png to PNG``` , ```ihdr to IHDR``` , ```idat to IDAT``` , ```iend to IEND``` by replacing with correct hexdump.
- Got the flag.

 <img width="1000" height="1000" alt="nutrela (2)" src="https://github.com/user-attachments/assets/7c503dca-ec61-4580-b8dd-8472a06f043e" />

## Concepts Learned:
- Got to know about hexdump of png file.
- learned how to correct it.


# 3. RAR of the Abyss:
Two philosophers peer into the networked abyss and swap a secret. Use the secret to decrypt the Abyss’ RAwR and pull your flag from the void.

## Flag:
```
nite{thus_sp0k3_th3_n3tw0rk_f0r3ns1cs_4n4lyst}
```

## Approach:
- Opened ```abyss.pcap``` file in wireshark.
- Analyzed the file and got the secret password exchanged between 2 philosophers - ```b3y0ndG00dand3vil```.
- Got a TCP packet having some RAR ASCII text.
- Followed that TCP stream and converted the format from ```ASCII``` to ```Raw```.
- Saved as a zipped file.
- Unzipped the zipped file using password- ```b3y0ndG00dand3vil``` using ```WINRAR``` application tool and got the flag.

## Concepts Learned:
- Learned how to analyse ```.pcap``` files using ```WIRESHARK``` tool.
  













