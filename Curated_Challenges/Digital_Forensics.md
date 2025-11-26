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
���6�>��:=����␦1�0���=������<␦�2���09����7�4���3������2�6���65����=�8��K9������8�:��m<1����3�<��������>�>��12=����␦9�0���5������4�2���89����?4���;������:�6���>␦5����5�8��[1�����0�:��}41����;�<��������6�>��Q:=����␦1�0���=������<␦�2�krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ steghide extract -sf sakamoto.jpg
Enter passphrase:
the file "flag.txt" does already exist. overwrite ? (y/n) y
wrote extracted data to "flag.txt".
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ cat flag.txt
nite{h1d3_4nd_s33k_but_w1th_st3g_sdfu9s8}
```

## Concepts Learned:
- Learned to use stegseek
- Got to know about wordlist ```rockyou.txt```.

