# Return Oriented Programming (ROP) notes
An exploitation technique typically employed when a stack-based buffer overflow
vulnerability exists. This consists of identifying "gadgets", which are simply
sets of CPU instructions that end with a `ret` instruction. By "chaining"
together several gadgets, an attacker can achieve arbitrary code execution.
A few examples of this technique include:

- Write data to memory and execute '/bin/bash' with the `execve` syscall
- Call a libc function (`ret2libc`)
- Use a `call <reg>` or `jmp <reg>` instruction to pass execution to shellcode
(`ret2reg`)
- Use a syscall to map writable memory, write the shellcode the memory
region, and then execute it

## Introduction to ROP
"Introduction to return oriented programming (ROP)", Code Arcana
- https://codearcana.com/posts/2013/05/28/introduction-to-return-oriented-programming-rop.html

## A very basic ret2reg example
Note: This is kind of difficult to read because of the screenshots, but is still
worth understanding.

"Stack Overflow ASLR bypass using ret2reg", sickness
- https://dl.packetstormsecurity.net/papers/attack/lewt2-aslrbypass.pdf

## ROP examples at ropemporium.com
- https://ropemporium.com/guide.html

## Writing shellcode to a mmap'ed region and executing it
"Exploit Writing Tutorial: ROP with Shellcode", Vincent Dary
- https://vincentdary.github.io/blog-posts/exploit-writing-tutorial-rop-with-shellcode/index.html

## Helpful ROP tricks, plus identifying ROP gadgets with radare2
"Basic ROP Techniques and Tricks", Josiah Pierce
- https://trustfoundry.net/basic-rop-techniques-and-tricks/

## ret2libc with an unknown libc at an unknown address
"Binary exploitation: ret2libc + unknown libc", Hugo "flawwan"
- https://tasteofsecurity.com/security/ret2libc-unknown-libc/

## Differences between 32-bit and 64-bit ROP
"Return Oriented Programming - Part2", Adwaith "adwait1-G" Gautham
- https://www.pwnthebox.net/reverse/engineering/and/binary/exploitation/series/2019/03/30/return-oriented-programming-part2.html

## Deep dive into ret2libc on 64-bit systems
"64-bit Linux Return-Oriented Programming", Ben Lynn
- https://crypto.stanford.edu/~blynn/rop/

## ROP chain with execve in a 64-bit Go application
"Smashing the Stack Part 2 - Building the ROP Chain", Danny "malwaresec"
Colmenares
- https://malwaresec.github.io/Building-the-ROP-Chain/
- https://github.com/MalwareSec/Building-the-ROP-Chain
