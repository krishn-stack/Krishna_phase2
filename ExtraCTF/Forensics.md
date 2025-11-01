# Riddle Registry:
Challenge given with a confidential.pdf file and asked to recover the flag.

## Flag:
```
picoCTF{puzzl3d_m3tadata_f0und!_c999e2a4}
```

## My Approach:
- Opened pdf file on an online pdf viewer.
- Got nothing behind the black lines in the pdf.
- Searched for .pdf file details.
- In Author details, there was some giberrish text so it needed to be decoded.

```
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ strings confidential.pdf
%PDF-1.7
1 0 obj
/Type /Pages
/Count 1
/Kids [ 4 0 R ]
endobj
2 0 obj
/Producer (PyPDF2)
/Author (cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9jOTk5ZTJhNH0\075)
endobj
3 0 obj
/Type /Catalog
/Pages 1 0 R
endobj
4 0 obj
/Type /Page
/Resources <<
/Font <<
/F1 5 0 R
```
- Opened ```https://www.base64decode.org/``` and decoded the text.

## My Learnings:
- Looking for the metadata of the .pdf file.
- decoding the metadata.


# Disko 3:
Given a .dd zipped file and asked to recover flag from that file.

## Flag:
```
picoCTF{n3v3r_z1p_2_h1d3_26d4f233}
```

## My Approach:
- Searched for .dd files
- Downloaded some softwares to work but didn't get much.
- Got some commands for zipped files and did things with those commands and got the flag.

## My Solve:

```
krishna@ULTRON:/tmp$ wget https://artifacts.picoctf.net/c/544/disko-3.dd.gz
--2025-11-01 19:23:05--  https://artifacts.picoctf.net/c/544/disko-3.dd.gz
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 18.67.161.8, 18.67.161.101, 18.67.161.65, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|18.67.161.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 20766078 (20M) [application/octet-stream]
Saving to: ‘disko-3.dd.gz’

disko-3.dd.gz        100%[===================>]  19.80M  2.29MB/s    in 9.4s

2025-11-01 19:23:16 (2.11 MB/s) - ‘disko-3.dd.gz’ saved [20766078/20766078]

krishna@ULTRON:/tmp$ gzip -d disko-3.dd.gz
krishna@ULTRON:/tmp$ file disko-3.dd
disko-3.dd: DOS/MBR boot sector, code offset 0x58+2, OEM-ID "mkfs.fat", Media descriptor 0xf8, sectors/track 32, heads 8, sectors 204800 (volumes > 32 MB), FAT (32 bit), sectors/FAT 1576, serial number 0x49838d0b, unlabeled
krishna@ULTRON:/tmp$ mmls disko-3.dd
Command 'mmls' not found, but can be installed with:
sudo apt install sleuthkit
krishna@ULTRON:/tmp$ sudo apt install sleuthkit
[sudo] password for krishna:
Sorry, try again.
[sudo] password for krishna:
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  libafflib0t64 libbfio1 libdate-manip-perl libewf2 libtsk19t64 libvhdi1
  libvmdk1
krishna@ULTRON:/tmp$ fls -r -p disko-3.dd
d/d 4:  log
d/d 22: log/private
d/d 24: log/sysstat
d/d 26: log/stunnel4
r/r 70: log/stunnel4/stunnel.log
d/d 28: log/mysql
d/d 30: log/inetsim
d/d 102:        log/inetsim/report
d/d 32: log/installer
d/d 134:        log/installer/cdebconf
r/r 150:        log/installer/cdebconf/questions.dat
r/r 152:        log/installer/cdebconf/templates.dat
r/r 136:        log/installer/Xorg.0.log
r/r 138:        log/installer/partman
r/r 140:        log/installer/syslog
r/r 143:        log/installer/hardware-summary
r/r 145:        log/installer/status
r/r 519091:     log/installer/lsb-release
r/r 519123:     log/vmware-vmsvc-root.2.log
r/r 519125:     log/kern.log.4.gz
r/r 519127:     log/Xorg.0.log
r/r 519130:     log/vmware-network.4.log
r/r 519132:     log/boot.log
r/r 519134:     log/syslog.3.gz
r/r 519137:     log/vmware-vmtoolsd-root.log
r/r 522627:     log/daemon.log
r/r 522628:     log/flag.gz
r/r * 522629:   log/_ESSAGES
r/r 522632:     log/alternatives.log.2.gz
r/r 522634:     log/debug
d/d 522636:     log/lightdm
r/r 554806:     log/lightdm/lightdm.log
r/r 554809:     log/lightdm/lightdm.log.old
r/r 554811:     log/lightdm/x-0.log
r/r 554813:     log/lightdm/x-0.log.old
r/r 554816:     log/lightdm/seat0-greeter.log
r/r 555203:     log/lightdm/seat0-greeter.log.old
r/r 522639:     log/vmware-network.6.log
r/r 522642:     log/alternatives.log
r/r 555285:     log/vmware-vmsvc-root.1.log
r/r 555288:     log/Xorg.0.log.old
r/r 555291:     log/vmware-network.8.log
r/r 555294:     log/vmware-vmsvc-root.log
r/r 555297:     log/vmware-vmsvc-root.3.log
r/r 556259:     log/boot.log.6
r/r 556262:     log/vmware-network.5.log
r/r 556265:     log/macchanger.log.4.gz
d/d 556267:     log/apt
r/r 556550:     log/apt/eipp.log.xz
r/r 556552:     log/apt/history.log
r/r 556554:     log/apt/term.log.2.gz
r/r 556557:     log/apt/history.log.5.gz
r/r 556559:     log/apt/term.log
r/r 556561:     log/apt/term.log.1.gz
r/r 561588:     log/apt/history.log.1.gz
r/r 561591:     log/apt/history.log.2.gz
r/r 561593:     log/apt/term.log.5.gz
r/r 561595:     log/apt/term.log.4.gz
r/r 561598:     log/apt/history.log.4.gz
r/r 561600:     log/apt/term.log.3.gz
r/r 572451:     log/apt/history.log.3.gz
r/r 556269:     log/dpkg.log.1
r/r 556271:     log/boot.log.5
r/r 556273:     log/wtmp
r/r 575571:     log/dpkg.log.5.gz
r/r 575573:     log/lastlog
r/r 575576:     log/vmware-network.3.log
r/r 575578:     log/syslog.4.gz
r/r 575580:     log/boot.log.1
r/r 575583:     log/vmware-network.2.log
r/r 575585:     log/faillog
r/r 603171:     log/kern.log.3.gz
r/r 603173:     log/dpkg.log.4.gz
r/r 603176:     log/vmware-network.1.log
r/r 603179:     log/vmware-network.7.log
d/d 603181:     log/journal
d/d 608872:     log/journal/480afdbb61874a758c0b53617cfc8e8f
r/r 608892:     log/journal/480afdbb61874a758c0b53617cfc8e8f/system@7a442d5ca4df4e0f9507094c9269ca6a-0000000000005a8a-0006054ede6dfcb2.journal
r/r 752228:     log/journal/480afdbb61874a758c0b53617cfc8e8f/system@d902d27452664082ae8a9ac82cb69ba1-0000000000004b19-0006054ecec0fb53.journal
r/r 752236:     log/journal/480afdbb61874a758c0b53617cfc8e8f/system@b0aa03528b9c43dc896b9ab01ba4c893-00000000000042ae-0006054ec01755dc.journal
r/r 1039652:    log/journal/480afdbb61874a758c0b53617cfc8e8f/system@fe4e86893ffe4006869e03921f0c0c32-00000000000052d8-0006054edbce9160.journal
r/r 1039660:    log/journal/480afdbb61874a758c0b53617cfc8e8f/system@54b9f53d65d44041abdf784998995b81-000000000000624c-0006054ef1ae82cf.journal
r/r 1324196:    log/journal/480afdbb61874a758c0b53617cfc8e8f/system@185d88d5eb13416d80fa5cb1c5faf4d0-000000000000a97e-00062a2783e88318.journal
r/r 1324199:    log/journal/480afdbb61874a758c0b53617cfc8e8f/user-1000.journal
r/r 1324207:    log/journal/480afdbb61874a758c0b53617cfc8e8f/system@185d88d5eb13416d80fa5cb1c5faf4d0-000000000001feae-00062ba433aaa6e0.journal
r/r 3225783:    log/journal/480afdbb61874a758c0b53617cfc8e8f/system@d902d27452664082ae8a9ac82cb69ba1-00000000000050fb-0006054ed43fd222.journal
r/r 3225791:    log/journal/480afdbb61874a758c0b53617cfc8e8f/system@24d583de9c1a4252813ff1f373a8814d-0000000000006989-00060561dfa7e3c8.journal
r/r 3225799:    log/journal/480afdbb61874a758c0b53617cfc8e8f/system@185d88d5eb13416d80fa5cb1c5faf4d0-00000000000070c7-0006224d2862127d.journal
r/r 3225807:    log/journal/480afdbb61874a758c0b53617cfc8e8f/user-1000@d902d27452664082ae8a9ac82cb69ba1-00000000000050fa-0006054ed43ef163.journal
r/r 3225815:    log/journal/480afdbb61874a758c0b53617cfc8e8f/user-1000@94309907b19d4653afc79e24b6eec039-00000000000005b4-0005e76be8304b42.journal
r/r 3225820:    log/journal/480afdbb61874a758c0b53617cfc8e8f/system@0006054e6fd33237-813b83aec6062020.journal~
r/r 3225828:    log/journal/480afdbb61874a758c0b53617cfc8e8f/user-1000@185d88d5eb13416d80fa5cb1c5faf4d0-000000000002374d-00062eff8e6c0038.journal
r/r 3225836:    log/journal/480afdbb61874a758c0b53617cfc8e8f/system@fe4e86893ffe4006869e03921f0c0c32-00000000000058b3-0006054edc51935b.journal
r/r 3225844:    log/journal/480afdbb61874a758c0b53617cfc8e8f/user-1000@fe4e86893ffe4006869e03921f0c0c32-00000000000058b2-0006054edc4fe35c.journal
r/r 3225849:    log/journal/480afdbb61874a758c0b53617cfc8e8f/user-1000@0006054e70c65fc3-7af43b1c79f1269a.journal~
r/r 3225857:    log/journal/480afdbb61874a758c0b53617cfc8e8f/system@7a442d5ca4df4e0f9507094c9269ca6a-000000000000605c-0006054ee0dded41.journal
r/r 603184:     log/vmware-network.log
r/r 603186:     log/dpkg.log.2.gz
v/v 3225859:    $MBR
v/v 3225860:    $FAT1
v/v 3225861:    $FAT2
V/V 3225862:    $OrphanFiles
krishna@ULTRON:/tmp$ icat disko-3.dd 522628 > flag.gz
krishna@ULTRON:/tmp$ ls
disko-3.dd
flag.gz
snap-private-tmp
systemd-private-b691b0f31ba94ce19dfb16fef72899e1-polkit.service-cNqMAD
systemd-private-b691b0f31ba94ce19dfb16fef72899e1-systemd-logind.service-kEeXrY
systemd-private-b691b0f31ba94ce19dfb16fef72899e1-systemd-resolved.service-vJZwPG
systemd-private-b691b0f31ba94ce19dfb16fef72899e1-systemd-timesyncd.service-V6ZQGO
systemd-private-b691b0f31ba94ce19dfb16fef72899e1-wsl-pro.service-SsIbhS
krishna@ULTRON:/tmp$ gzip -d flag.gz
krishna@ULTRON:/tmp$ cat flag
Here is your flag
picoCTF{n3v3r_z1p_2_h1d3_26d4f233}
```

## My Learnings:
- Learnt about new wsl commands.
- Learnt how to deal with .dd files.
