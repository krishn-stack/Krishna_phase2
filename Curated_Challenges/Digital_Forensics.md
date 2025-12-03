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
- Got a ```TCP``` packet having some ```RA R ASCII``` text.
- Followed that TCP stream and converted the format from ```ASCII``` to ```Raw```.
- Saved as a zipped file.
- Unzipped the zipped file using password- ```b3y0ndG00dand3vil``` using ```WINRAR``` application tool and got the flag.

## Concepts Learned:
- Learned how to analyse ```.pcap``` files using ```WIRESHARK``` tool.


# 4. NineTails:
Looks like I got a little too clever and hid the flag as a password in Firefox, tucked away like one of NineTails’ many tails. Recover the "logins" and the "key4" and let it guide you to the flag.

Hint:
I named my Ninetails "j4gjesg4", quite a peculiar name isn't it?

## Flag:
```
GCTF{m0zarella_f1ref0x_p4ssw0rd}
```

## Approach;
- Given a ```.rar``` challenge file, unzipped it using ```WINRAR``` application.
- Got a ```ninetails.ad1``` file.
- Searched about ```.ad1``` files and got to know about how to access it using ```Exterro FTK Imager``` tool.
- Exported the contents of ```ninetails.ad1``` file into my local machine.
- In the folder exported from ```FTK Imager```, searched for ```logins.json``` and ```key4.db``` file.
- Followed this path- ``` C:\Users\Krishna\Downloads\ninetails\GIC2024\AppData\Roaming\Mozilla\Firefox\Profiles\j4gjesg4.default-release ```.
- Got ```logins.json``` and ```key4.db``` in ```j4gjesg4.default-release```.
- Downloaded Mozilla Firefox browser.
- Logins.json file had some encrypted username and password which has to be decrypted using key4.db file.
- Opened Mozilla Firefox, went to ```Help -> More Troubleshooting information -> Open Folder in Profile Folder -> nqddew2u.default-release folder opened -> replaced logins and key4 file with our extracted files -> Opened Passwords in browser -> Got the flag ```.

## Concepts Learned:
- Learned about ```logins``` and ```key4``` files in password management.
- How to decrypt them.


# 5. Re:Draw:
Her screen went black and a strange command window flickered to life, lines of text flashed across before everything went silent. Moments later, the system crashed. By sheer luck, we recovered a memory dump. 

Note: There are three stages to this challenge and you will find three flags.

What we know: just before the crash, a black command window flickered across the screen, something in its output might still be visible if you dig through memory. She was drawing when it happened, and remnants of a painting program linger, which could reveal more if inspected in the right way. Finally, a mysterious archive hides deeper in memory, likely holding the last piece of her work.

Hint:
Learn up on volatility 2 and its various plugins and what they are used for.


## Flags:
```
flag{th1s_1s_th3_1st_st4g3!!}
flag{Good_BoY_good_girL}
flag{w3Il_3rd_stage_was_easy}
```

## Approach:
- Used volatility tool as suggeseted in hint.
- Got a Base4 encrypted text- ```ZmxhZ3t0aDFzXzFzX3RoM18xc3Rfc3Q0ZzMhIX0=```, decrypted it using ```CyberChef``` and got first flag.
- ```memdump``` the process id ```(PID)```of ```mspaint.exe``` which was ```2424``` as description says before crashing some drawing was happening.
- Opened ```2424.data``` file using ```GIMP``` tool, got an image.

<img width="1332" height="547" alt="Screenshot 2025-12-03 154414" src="https://github.com/user-attachments/assets/c9e13273-2fe0-4ef4-94b3-dba52903d57d" />

- Investigated third file ```WinRar.exe``` file and got ```Important.rar``` files and dumped this file using ```dumpfiles``` plug-in.
- Tried unzipping the extracted zipped file using a hash password as it says- ```CMTPassword is NTLM hash(in uppercase) of Alissa's account passwd```.
- Found the NTLM hash using ```hashdump``` plugin, changed into uppercase letters and found the flag.

  <img width="500" height="500" alt="flag3" src="https://github.com/user-attachments/assets/5bc7ef3b-d7e4-4dbb-84c6-26babd4e606d" />

## Plug-ins used:
- ```imageinfo``` - Identify information for the image.
- ```pslist``` - Print all running processes by following the EPROCESS lists.
- ```cmdscan``` - Extract command history by scanning for _COMMAND_HISTORY.
- ```consoles``` - Extract command history by scanning for _CONSOLE_INFORMATION.
- ```memdump``` - Dump the addressable memory for a process.
- ```cmdline``` - Display process command-line arguments.
- ```filescan``` - Pool scanner for file objects.
- ```dumpfiles``` - Extract memory mapped and cached files.
- ```hashdump``` - Dumps passwords hashes (LM/NTLM) from memory.

## Concepts Learned:
- Learned about ```Volatility 2.6``` tool for ```Memory Forensics```.
- Learned about its plug-ins and their usage.


## My Solve:

```
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ file MemoryDump_Lab1.raw
MemoryDump_Lab1.raw: data
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ cd volatility_2.6/
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads/volatility_2.6$ ./volatility_2.6_win64_standalone.exe
Volatility Foundation Volatility Framework 2.6
ERROR   : volatility.debug    : You must specify something to do (try -h)
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads/volatility_2.6$ ./volatility_2.6_win64_standalone.exe --help
Volatility Foundation Volatility Framework 2.6
Usage: Volatility - A memory forensics analysis platform.

Options:
  -h, --help            list all available options and their default values.
                        Default values may be set in the configuration file
                        (/etc/volatilityrc)
  --conf-file=.volatilityrc
                        User based configuration file
  -d, --debug           Debug volatility
  --plugins=PLUGINS     Additional plugin directories to use (semi-colon
                        separated)
  --info                Print information about all registered objects
  --cache-directory=C:\Users\Krishna/.cache\volatility
                        Directory where cache files are stored
  --cache               Use caching
  --tz=TZ               Sets the (Olson) timezone for displaying timestamps
                        using pytz (if installed) or tzset
  -f FILENAME, --filename=FILENAME
                        Filename to use when opening an image
  --profile=WinXPSP2x86
                        Name of the profile to load (use --info to see a list
                        of supported profiles)
  -l LOCATION, --location=LOCATION
                        A URN location from which to load an address space
  -w, --write           Enable write support
  --dtb=DTB             DTB Address
  --shift=SHIFT         Mac KASLR shift address
  --output=text         Output in this format (support is module specific, see
                        the Module Output Options below)
  --output-file=OUTPUT_FILE
                        Write output in this file
  -v, --verbose         Verbose information
  -g KDBG, --kdbg=KDBG  Specify a KDBG virtual address (Note: for 64-bit
                        Windows 8 and above this is the address of
                        KdCopyDataBlock)
  --force               Force utilization of suspect profile
  -k KPCR, --kpcr=KPCR  Specify a specific KPCR address
  --cookie=COOKIE       Specify the address of nt!ObHeaderCookie (valid for
                        Windows 10 only)

        Supported Plugin Commands:

                amcache         Print AmCache information
                apihooks        Detect API hooks in process and kernel memory
                atoms           Print session and window station atom tables
                atomscan        Pool scanner for atom tables
                auditpol        Prints out the Audit Policies from HKLM\SECURITY\Policy\PolAdtEv
                bigpools        Dump the big page pools using BigPagePoolScanner
                bioskbd         Reads the keyboard buffer from Real Mode memory
                cachedump       Dumps cached domain hashes from memory
                callbacks       Print system-wide notification routines
                clipboard       Extract the contents of the windows clipboard
                cmdline         Display process command-line arguments
                cmdscan         Extract command history by scanning for _COMMAND_HISTORY
                connections     Print list of open connections [Windows XP and 2003 Only]
                connscan        Pool scanner for tcp connections
                consoles        Extract command history by scanning for _CONSOLE_INFORMATION
                crashinfo       Dump crash-dump information
                deskscan        Poolscaner for tagDESKTOP (desktops)
                devicetree      Show device tree
                dlldump         Dump DLLs from a process address space
                dlllist         Print list of loaded dlls for each process
                driverirp       Driver IRP hook detection
                drivermodule    Associate driver objects to kernel modules
                driverscan      Pool scanner for driver objects
                dumpcerts       Dump RSA private and public SSL keys
                dumpfiles       Extract memory mapped and cached files
                dumpregistry    Dumps registry files out to disk
                editbox         Displays information about Edit controls. (Listbox experimental.)
                envars          Display process environment variables
                eventhooks      Print details on windows event hooks
                evtlogs         Extract Windows Event Logs (XP/2003 only)
                filescan        Pool scanner for file objects
                gahti           Dump the USER handle type information
                gditimers       Print installed GDI timers and callbacks
                gdt             Display Global Descriptor Table
                getservicesids  Get the names of services in the Registry and return Calculated SID
                getsids         Print the SIDs owning each process
                handles         Print list of open handles for each process
                hashdump        Dumps passwords hashes (LM/NTLM) from memory
                hibinfo         Dump hibernation file information
                hivedump        Prints out a hive
                hivelist        Print list of registry hives.
                hivescan        Pool scanner for registry hives
                hpakextract     Extract physical memory from an HPAK file
                hpakinfo        Info on an HPAK file
                idt             Display Interrupt Descriptor Table
                iehistory       Reconstruct Internet Explorer cache / history
                imagecopy       Copies a physical address space out as a raw DD image
                imageinfo       Identify information for the image
                impscan         Scan for calls to imported functions
                joblinks        Print process job link information
                kdbgscan        Search for and dump potential KDBG values
                kpcrscan        Search for and dump potential KPCR values
                ldrmodules      Detect unlinked DLLs
                lsadump         Dump (decrypted) LSA secrets from the registry
                machoinfo       Dump Mach-O file format information
                malfind         Find hidden and injected code
                mbrparser       Scans for and parses potential Master Boot Records (MBRs)
                memdump         Dump the addressable memory for a process
                memmap          Print the memory map
                messagehooks    List desktop and thread window message hooks
                mftparser       Scans for and parses potential MFT entries
                moddump         Dump a kernel driver to an executable file sample
                modscan         Pool scanner for kernel modules
                modules         Print list of loaded modules
                multiscan       Scan for various objects at once
                mutantscan      Pool scanner for mutex objects
                notepad         List currently displayed notepad text
                objtypescan     Scan for Windows object type objects
                patcher         Patches memory based on page scans
                poolpeek        Configurable pool scanner plugin
                printkey        Print a registry key, and its subkeys and values
                privs           Display process privileges
                procdump        Dump a process to an executable file sample
                pslist          Print all running processes by following the EPROCESS lists
                psscan          Pool scanner for process objects
                pstree          Print process list as a tree
                psxview         Find hidden processes with various process listings
                qemuinfo        Dump Qemu information
                raw2dmp         Converts a physical memory sample to a windbg crash dump
                screenshot      Save a pseudo-screenshot based on GDI windows
                servicediff     List Windows services (ala Plugx)
                sessions        List details on _MM_SESSION_SPACE (user logon sessions)
                shellbags       Prints ShellBags info
                shimcache       Parses the Application Compatibility Shim Cache registry key
                shutdowntime    Print ShutdownTime of machine from registry
                sockets         Print list of open sockets
                sockscan        Pool scanner for tcp socket objects
                ssdt            Display SSDT entries
                strings         Match physical offsets to virtual addresses (may take a while, VERY verbose)
                svcscan         Scan for Windows services
                symlinkscan     Pool scanner for symlink objects
                thrdscan        Pool scanner for thread objects
                threads         Investigate _ETHREAD and _KTHREADs
                timeliner       Creates a timeline from various artifacts in memory
                timers          Print kernel timers and associated module DPCs
                truecryptmaster Recover TrueCrypt 7.1a Master Keys
                truecryptpassphrase     TrueCrypt Cached Passphrase Finder
                truecryptsummary        TrueCrypt Summary
                unloadedmodules Print list of unloaded modules
                userassist      Print userassist registry keys and information
                userhandles     Dump the USER handle tables
                vaddump         Dumps out the vad sections to a file
                vadinfo         Dump the VAD info
                vadtree         Walk the VAD tree and display in tree format
                vadwalk         Walk the VAD tree
                vboxinfo        Dump virtualbox information
                verinfo         Prints out the version information from PE images
                vmwareinfo      Dump VMware VMSS/VMSN information
                volshell        Shell in the memory image
                windows         Print Desktop Windows (verbose details)
                wintree         Print Z-Order Desktop Windows Tree
                wndscan         Pool scanner for window stations
                yarascan        Scan process or kernel memory with Yara signatures
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads/volatility_2.6$ cd ..
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ volatility -f MemoryDump_Lab1.raw imageinfo
Command 'volatility' not found, but can be installed with:
sudo snap install volatility-phocean
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ sudo snap install volatility-phocean
[sudo] password for krishna:
2025-12-03T09:21:08Z INFO Waiting for automatic snapd restart...
volatility-phocean git-master from Jean-Christophe Baptiste (jc-baptiste) installed
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ volatility -f MemoryDump_Lab1.raw imageinfo
Volatility Foundation Volatility Framework 2.6.1
INFO    : volatility.debug    : Determining profile based on KDBG search...
          Suggested Profile(s) : Win7SP1x64, Win7SP0x64, Win2008R2SP0x64, Win2008R2SP1x64_24000, Win2008R2SP1x64_23418, Win2008R2SP1x64, Win7SP1x64_24000, Win7SP1x64_23418
                     AS Layer1 : WindowsAMD64PagedMemory (Kernel AS)
                     AS Layer2 : FileAddressSpace (/mnt/c/Users/Krishna/Downloads/MemoryDump_Lab1.raw)
                      PAE type : No PAE
                           DTB : 0x187000L
                          KDBG : 0xf800028100a0L
          Number of Processors : 1
     Image Type (Service Pack) : 1
                KPCR for CPU 0 : 0xfffff80002811d00L
             KUSER_SHARED_DATA : 0xfffff78000000000L
           Image date and time : 2019-12-11 14:38:00 UTC+0000
     Image local date and time : 2019-12-11 20:08:00 +0530
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ volatility -f MemoryDump_Lab1.raw --profile=Win7SP1x64 pslist
Volatility Foundation Volatility Framework 2.6.1
Offset(V)          Name                    PID   PPID   Thds     Hnds   Sess  Wow64 Start                          Exit
------------------ -------------------- ------ ------ ------ -------- ------ ------ ------------------------------ ------------------------------
0xfffffa8000ca0040 System                    4      0     80      570 ------      0 2019-12-11 13:41:25 UTC+0000
0xfffffa800148f040 smss.exe                248      4      3       37 ------      0 2019-12-11 13:41:25 UTC+0000
0xfffffa800154f740 csrss.exe               320    312      9      457      0      0 2019-12-11 13:41:32 UTC+0000
0xfffffa8000ca81e0 csrss.exe               368    360      7      199      1      0 2019-12-11 13:41:33 UTC+0000
0xfffffa8001c45060 psxss.exe               376    248     18      786      0      0 2019-12-11 13:41:33 UTC+0000
0xfffffa8001c5f060 winlogon.exe            416    360      4      118      1      0 2019-12-11 13:41:34 UTC+0000
0xfffffa8001c5f630 wininit.exe             424    312      3       75      0      0 2019-12-11 13:41:34 UTC+0000
0xfffffa8001c98530 services.exe            484    424     13      219      0      0 2019-12-11 13:41:35 UTC+0000
0xfffffa8001ca0580 lsass.exe               492    424      9      764      0      0 2019-12-11 13:41:35 UTC+0000
0xfffffa8001ca4b30 lsm.exe                 500    424     11      185      0      0 2019-12-11 13:41:35 UTC+0000
0xfffffa8001cf4b30 svchost.exe             588    484     11      358      0      0 2019-12-11 13:41:39 UTC+0000
0xfffffa8001d327c0 VBoxService.ex          652    484     13      137      0      0 2019-12-11 13:41:40 UTC+0000
0xfffffa8001d49b30 svchost.exe             720    484      8      279      0      0 2019-12-11 13:41:41 UTC+0000
0xfffffa8001d8c420 svchost.exe             816    484     23      569      0      0 2019-12-11 13:41:42 UTC+0000
0xfffffa8001da5b30 svchost.exe             852    484     28      542      0      0 2019-12-11 13:41:43 UTC+0000
0xfffffa8001da96c0 svchost.exe             876    484     32      941      0      0 2019-12-11 13:41:43 UTC+0000
0xfffffa8001e1bb30 svchost.exe             472    484     19      476      0      0 2019-12-11 13:41:47 UTC+0000
0xfffffa8001e50b30 svchost.exe            1044    484     14      366      0      0 2019-12-11 13:41:48 UTC+0000
0xfffffa8001eba230 spoolsv.exe            1208    484     13      282      0      0 2019-12-11 13:41:51 UTC+0000
0xfffffa8001eda060 svchost.exe            1248    484     19      313      0      0 2019-12-11 13:41:52 UTC+0000
0xfffffa8001f58890 svchost.exe            1372    484     22      295      0      0 2019-12-11 13:41:54 UTC+0000
0xfffffa8001f91b30 TCPSVCS.EXE            1416    484      4       97      0      0 2019-12-11 13:41:55 UTC+0000
0xfffffa8000d3c400 sppsvc.exe             1508    484      4      141      0      0 2019-12-11 14:16:06 UTC+0000
0xfffffa8001c38580 svchost.exe             948    484     13      322      0      0 2019-12-11 14:16:07 UTC+0000
0xfffffa8002170630 wmpnetwk.exe           1856    484     16      451      0      0 2019-12-11 14:16:08 UTC+0000
0xfffffa8001d376f0 SearchIndexer.          480    484     14      701      0      0 2019-12-11 14:16:09 UTC+0000
0xfffffa8001eb47f0 taskhost.exe            296    484      8      151      1      0 2019-12-11 14:32:24 UTC+0000
0xfffffa8001dfa910 dwm.exe                1988    852      5       72      1      0 2019-12-11 14:32:25 UTC+0000
0xfffffa8002046960 explorer.exe            604   2016     33      927      1      0 2019-12-11 14:32:25 UTC+0000
0xfffffa80021c75d0 VBoxTray.exe           1844    604     11      140      1      0 2019-12-11 14:32:35 UTC+0000
0xfffffa80021da060 audiodg.exe            2064    816      6      131      0      0 2019-12-11 14:32:37 UTC+0000
0xfffffa80022199e0 svchost.exe            2368    484      9      365      0      0 2019-12-11 14:32:51 UTC+0000
0xfffffa8002222780 cmd.exe                1984    604      1       21      1      0 2019-12-11 14:34:54 UTC+0000
0xfffffa8002227140 conhost.exe            2692    368      2       50      1      0 2019-12-11 14:34:54 UTC+0000
0xfffffa80022bab30 mspaint.exe            2424    604      6      128      1      0 2019-12-11 14:35:14 UTC+0000
0xfffffa8000eac770 svchost.exe            2660    484      6      100      0      0 2019-12-11 14:35:14 UTC+0000
0xfffffa8001e68060 csrss.exe              2760   2680      7      172      2      0 2019-12-11 14:37:05 UTC+0000
0xfffffa8000ecbb30 winlogon.exe           2808   2680      4      119      2      0 2019-12-11 14:37:05 UTC+0000
0xfffffa8000f3aab0 taskhost.exe           2908    484      9      158      2      0 2019-12-11 14:37:13 UTC+0000
0xfffffa8000f4db30 dwm.exe                3004    852      5       72      2      0 2019-12-11 14:37:14 UTC+0000
0xfffffa8000f4c670 explorer.exe           2504   3000     34      825      2      0 2019-12-11 14:37:14 UTC+0000
0xfffffa8000f9a4e0 VBoxTray.exe           2304   2504     14      144      2      0 2019-12-11 14:37:14 UTC+0000
0xfffffa8000fff630 SearchProtocol         2524    480      7      226      2      0 2019-12-11 14:37:21 UTC+0000
0xfffffa8000ecea60 SearchFilterHo         1720    480      5       90      0      0 2019-12-11 14:37:21 UTC+0000
0xfffffa8001010b30 WinRAR.exe             1512   2504      6      207      2      0 2019-12-11 14:37:23 UTC+0000
0xfffffa8001020b30 SearchProtocol         2868    480      8      279      0      0 2019-12-11 14:37:23 UTC+0000
0xfffffa8001048060 DumpIt.exe              796    604      2       45      1      1 2019-12-11 14:37:54 UTC+0000
0xfffffa800104a780 conhost.exe            2260    368      2       50      1      0 2019-12-11 14:37:54 UTC+0000
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ volatility -f MemoryDump_Lab1.raw --profile=Win7SP1x64 cmdscan
Volatility Foundation Volatility Framework 2.6.1
**************************************************
CommandProcess: conhost.exe Pid: 2692
CommandHistory: 0x1fe9c0 Application: cmd.exe Flags: Allocated, Reset
CommandCount: 1 LastAdded: 0 LastDisplayed: 0
FirstCommand: 0 CommandCountMax: 50
ProcessHandle: 0x60
Cmd #0 @ 0x1de3c0: St4G3$1
Cmd #15 @ 0x1c0158:
Cmd #16 @ 0x1fdb30:
**************************************************
CommandProcess: conhost.exe Pid: 2260
CommandHistory: 0x38ea90 Application: DumpIt.exe Flags: Allocated
CommandCount: 0 LastAdded: -1 LastDisplayed: -1
FirstCommand: 0 CommandCountMax: 50
ProcessHandle: 0x60
Cmd #15 @ 0x350158: 8
Cmd #16 @ 0x38dc00: 8
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ volatility -f MemoryDump_Lab1.raw --profile=Win7SP1x64 consoles
Volatility Foundation Volatility Framework 2.6.1
**************************************************
ConsoleProcess: conhost.exe Pid: 2692
Console: 0xff756200 CommandHistorySize: 50
HistoryBufferCount: 1 HistoryBufferMax: 4
OriginalTitle: %SystemRoot%\system32\cmd.exe
Title: C:\Windows\system32\cmd.exe - St4G3$1
AttachedProcess: cmd.exe Pid: 1984 Handle: 0x60
----
CommandHistory: 0x1fe9c0 Application: cmd.exe Flags: Allocated, Reset
CommandCount: 1 LastAdded: 0 LastDisplayed: 0
FirstCommand: 0 CommandCountMax: 50
ProcessHandle: 0x60
Cmd #0 at 0x1de3c0: St4G3$1
----
Screen 0x1e0f70 X:80 Y:300
Dump:
Microsoft Windows [Version 6.1.7601]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\Users\SmartNet>St4G3$1
ZmxhZ3t0aDFzXzFzX3RoM18xc3Rfc3Q0ZzMhIX0=
Press any key to continue . . .

**************************************************
ConsoleProcess: conhost.exe Pid: 2260
Console: 0xff756200 CommandHistorySize: 50
HistoryBufferCount: 1 HistoryBufferMax: 4
OriginalTitle: C:\Users\SmartNet\Downloads\DumpIt\DumpIt.exe
Title: C:\Users\SmartNet\Downloads\DumpIt\DumpIt.exe
AttachedProcess: DumpIt.exe Pid: 796 Handle: 0x60
----
CommandHistory: 0x38ea90 Application: DumpIt.exe Flags: Allocated
CommandCount: 0 LastAdded: -1 LastDisplayed: -1
FirstCommand: 0 CommandCountMax: 50
ProcessHandle: 0x60
----
Screen 0x371050 X:80 Y:300
Dump:
  DumpIt - v1.3.2.20110401 - One click memory memory dumper
  Copyright (c) 2007 - 2011, Matthieu Suiche <http://www.msuiche.net>
  Copyright (c) 2010 - 2011, MoonSols <http://www.moonsols.com>


    Address space size:        1073676288 bytes (   1023 Mb)
    Free space size:          24185389056 bytes (  23064 Mb)

    * Destination = \??\C:\Users\SmartNet\Downloads\DumpIt\SMARTNET-PC-20191211-
143755.raw

    --> Are you sure you want to continue? [y/n] y
    + Processing...
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ volatility -f MemoryDump_Lab1.raw --profile=Win7SP1x64 mspaintscan
Volatility Foundation Volatility Framework 2.6.1
ERROR   : volatility.debug    : You must specify something to do (try -h)
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ volatility -f MemoryDump_Lab1.raw --profile=Win7SP1x64 memdump -p 2424 -D ./redraw
Volatility Foundation Volatility Framework 2.6.1
************************************************************************
Writing mspaint.exe [  2424] to 2424.dmp
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ mv 2424.dmp 2424.data
mv: cannot stat '2424.dmp': No such file or directory
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ cd redraw/
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads/redraw$ mv 2424.dmp 2424.data
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads/redraw$ cd ..
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ volatility -f MemoryDump_Lab1.raw --profile=Win7SP1x64 cmdline
Volatility Foundation Volatility Framework 2.6.1
************************************************************************
System pid:      4
************************************************************************
smss.exe pid:    248
Command line : \SystemRoot\System32\smss.exe
************************************************************************
csrss.exe pid:    320
Command line : %SystemRoot%\system32\csrss.exe ObjectDirectory=\Windows SharedSection=1024,20480,768 Windows=On SubSystemType=Windows ServerDll=basesrv,1 ServerDll=winsrv:UserServerDllInitialization,3 ServerDll=winsrv:ConServerDllInitialization,2 ServerDll=sxssrv,4 ProfileControl=Off MaxRequestThreads=16
************************************************************************
csrss.exe pid:    368
Command line : %SystemRoot%\system32\csrss.exe ObjectDirectory=\Windows SharedSection=1024,20480,768 Windows=On SubSystemType=Windows ServerDll=basesrv,1 ServerDll=winsrv:UserServerDllInitialization,3 ServerDll=winsrv:ConServerDllInitialization,2 ServerDll=sxssrv,4 ProfileControl=Off MaxRequestThreads=16
************************************************************************
psxss.exe pid:    376
Command line : %SystemRoot%\system32\psxss.exe
************************************************************************
winlogon.exe pid:    416
Command line : winlogon.exe
************************************************************************
wininit.exe pid:    424
Command line : wininit.exe
************************************************************************
services.exe pid:    484
Command line : C:\Windows\system32\services.exe
************************************************************************
lsass.exe pid:    492
Command line : C:\Windows\system32\lsass.exe
************************************************************************
lsm.exe pid:    500
Command line : C:\Windows\system32\lsm.exe
************************************************************************
svchost.exe pid:    588
Command line : C:\Windows\system32\svchost.exe -k DcomLaunch
************************************************************************
VBoxService.ex pid:    652
Command line : C:\Windows\System32\VBoxService.exe
************************************************************************
svchost.exe pid:    720
Command line : C:\Windows\system32\svchost.exe -k RPCSS
************************************************************************
svchost.exe pid:    816
Command line : C:\Windows\System32\svchost.exe -k LocalServiceNetworkRestricted
************************************************************************
svchost.exe pid:    852
Command line : C:\Windows\System32\svchost.exe -k LocalSystemNetworkRestricted
************************************************************************
svchost.exe pid:    876
Command line : C:\Windows\system32\svchost.exe -k netsvcs
************************************************************************
svchost.exe pid:    472
Command line : C:\Windows\system32\svchost.exe -k LocalService
************************************************************************
svchost.exe pid:   1044
Command line : C:\Windows\system32\svchost.exe -k NetworkService
************************************************************************
spoolsv.exe pid:   1208
Command line : C:\Windows\System32\spoolsv.exe
************************************************************************
svchost.exe pid:   1248
Command line : C:\Windows\system32\svchost.exe -k LocalServiceNoNetwork
************************************************************************
svchost.exe pid:   1372
Command line : C:\Windows\system32\svchost.exe -k LocalServiceAndNoImpersonation
************************************************************************
TCPSVCS.EXE pid:   1416
Command line : C:\Windows\System32\tcpsvcs.exe
************************************************************************
sppsvc.exe pid:   1508
Command line : C:\Windows\system32\sppsvc.exe
************************************************************************
svchost.exe pid:    948
Command line : C:\Windows\System32\svchost.exe -k secsvcs
************************************************************************
wmpnetwk.exe pid:   1856
Command line : "C:\Program Files\Windows Media Player\wmpnetwk.exe"
************************************************************************
SearchIndexer. pid:    480
Command line : C:\Windows\system32\SearchIndexer.exe /Embedding
************************************************************************
taskhost.exe pid:    296
Command line : "taskhost.exe"
************************************************************************
dwm.exe pid:   1988
Command line : "C:\Windows\system32\Dwm.exe"
************************************************************************
explorer.exe pid:    604
Command line : C:\Windows\Explorer.EXE
************************************************************************
VBoxTray.exe pid:   1844
Command line : "C:\Windows\System32\VBoxTray.exe"
************************************************************************
audiodg.exe pid:   2064
Command line : C:\Windows\system32\AUDIODG.EXE 0x20c
************************************************************************
svchost.exe pid:   2368
Command line : C:\Windows\System32\svchost.exe -k LocalServicePeerNet
************************************************************************
cmd.exe pid:   1984
Command line : "C:\Windows\system32\cmd.exe"
************************************************************************
conhost.exe pid:   2692
Command line : \??\C:\Windows\system32\conhost.exe
************************************************************************
mspaint.exe pid:   2424
Command line : "C:\Windows\system32\mspaint.exe"
************************************************************************
svchost.exe pid:   2660
Command line : C:\Windows\system32\svchost.exe -k imgsvc
************************************************************************
csrss.exe pid:   2760
Command line : %SystemRoot%\system32\csrss.exe ObjectDirectory=\Windows SharedSection=1024,20480,768 Windows=On SubSystemType=Windows ServerDll=basesrv,1 ServerDll=winsrv:UserServerDllInitialization,3 ServerDll=winsrv:ConServerDllInitialization,2 ServerDll=sxssrv,4 ProfileControl=Off MaxRequestThreads=16
************************************************************************
winlogon.exe pid:   2808
Command line : winlogon.exe
************************************************************************
taskhost.exe pid:   2908
Command line : "taskhost.exe"
************************************************************************
dwm.exe pid:   3004
Command line : "C:\Windows\system32\Dwm.exe"
************************************************************************
explorer.exe pid:   2504
Command line : C:\Windows\Explorer.EXE
************************************************************************
VBoxTray.exe pid:   2304
Command line : "C:\Windows\System32\VBoxTray.exe"
************************************************************************
SearchProtocol pid:   2524
Command line : "C:\Windows\system32\SearchProtocolHost.exe" Global\UsGthrFltPipeMssGthrPipe_S-1-5-21-3073570648-3149397540-2269648332-10032_ Global\UsGthrCtrlFltPipeMssGthrPipe_S-1-5-21-3073570648-3149397540-2269648332-10032 1 -2147483646 "Software\Microsoft\Windows Search" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT; MS Search 4.0 Robot)" "C:\ProgramData\Microsoft\Search\Data\Temp\usgthrsvc" "DownLevelDaemon"  "1"
************************************************************************
SearchFilterHo pid:   1720
Command line : "C:\Windows\system32\SearchFilterHost.exe" 0 508 512 520 65536 516
************************************************************************
WinRAR.exe pid:   1512
Command line : "C:\Program Files\WinRAR\WinRAR.exe" "C:\Users\Alissa Simpson\Documents\Important.rar"
************************************************************************
SearchProtocol pid:   2868
Command line : "C:\Windows\system32\SearchProtocolHost.exe" Global\UsGthrFltPipeMssGthrPipe3_ Global\UsGthrCtrlFltPipeMssGthrPipe3 1 -2147483646 "Software\Microsoft\Windows Search" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT; MS Search 4.0 Robot)" "C:\ProgramData\Microsoft\Search\Data\Temp\usgthrsvc" "DownLevelDaemon"
************************************************************************
DumpIt.exe pid:    796
Command line : "C:\Users\SmartNet\Downloads\DumpIt\DumpIt.exe"
************************************************************************
conhost.exe pid:   2260
Command line : \??\C:\Windows\system32\conhost.exe
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ volatility -f MemoryDump_Lab1.raw --profile=Win7SP1x64 filescan
Volatility Foundation Volatility Framework 2.6.1
0x000000003fa3ebc0      1      0 R--r-- \Device\HarddiskVolume2\Users\Alissa Simpson\Documents\Important.rar
0x000000003fac3bc0      1      0 R--r-- \Device\HarddiskVolume2\Users\Alissa Simpson\Documents\Important.rar
0x000000003fb48bc0      1      0 R--r-- \Device\HarddiskVolume2\Users\Alissa Simpson\Documents\Important.rar
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ volatility -f MemoryDump_Lab1.raw --profile=Win7SP1x64 dumpfiles -Q 0x000000003fa3ebc0 -D ./redraw/
Volatility Foundation Volatility Framework 2.6.1
DataSectionObject 0x3fa3ebc0   None   \Device\HarddiskVolume2\Users\Alissa Simpson\Documents\Important.rar

krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ cd redraw/
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads/redraw$ lss
Command 'lss' not found, but there are 16 similar ones.
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads/redraw$ ls
2424.data  MemoryDump_Lab1.raw  file.None.0xfffffa8001034450.dat
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads/redraw$ file file.None.0xfffffa8001034450.dat
file.None.0xfffffa8001034450.dat: RAR archive data, v5
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads/redraw$ mv file.None.0xfffffa8001034450.dat winfile.rar
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads/redraw$ ls
2424.data  MemoryDump_Lab1.raw  winfile.rar
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads/redraw$ strings winfile.rar
Rar!
CMTPassword is NTLM hash(in uppercase) of Alissa's account passwd.
        flag3.png0

krishna@ULTRON:/mnt/c/Users/Krishna/Downloads/redraw$ volatility -f MemoryDump_Lab1.raw --profile=Win7SP1x64 hashdump
Volatility Foundation Volatility Framework 2.6.1
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
SmartNet:1001:aad3b435b51404eeaad3b435b51404ee:4943abb39473a6f32c11301f4987e7e0:::
HomeGroupUser$:1002:aad3b435b51404eeaad3b435b51404ee:f0fc3d257814e08fea06e63c5762ebd5:::
Alissa Simpson:1003:aad3b435b51404eeaad3b435b51404ee:f4ff64c8baac57d22f22edc681055ba6:::
```






























