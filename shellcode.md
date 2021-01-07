# Shellcode notes
Various notes about "shellcode", or assembly used in an exploit payload to
execute a shell session, or build a new program. This term remains,
unfortunately, very nebulous.

In "The Shellcoder's Handbook", Anley et al. states:
```
"The term shellcode is derived from its original purpose - it was the specific
portion of an exploit used to spawn a root shell. This is still the most common 
type of shellcode used, but many programmers have refined shellcode to
do more[.]" - Page 41
```

Essentially think of it as an optional portion of a payload used in an exploit
to add new functionality to the target software.

#### Metasploit shellcode encoder behavior
"Analyzing Metasploit Payloads", Niels van Gijzen
- https://hatching.io/blog/metasploit-payloads2/

#### Analysis of 64-bit Metasploit shellcode
"X64 Linux Metasploit execve /bin/sh Shellcode Analysis", epibar052
- https://epi052.gitlab.io/notes-to-self/blog/2018-08-04-x64-linux-metasploit-execve-bin-sh-shellcode-analysis/
