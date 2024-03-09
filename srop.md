# Sigreturn Oriented Programming

A method of return-oriented programming that relies on the sigreturn(2)
system call. A hacker first places a sigcontext / ucontext object on
the stack. This object specifies CPU register values and other process
state that will be set when the sigreturn system call executes.

The hacker then executes the sigreturn system call using a syscall or
int ROP gadget. The kernel then sets CPU registers and process state
to the hacker-specified values found in the sigcontext object.

On a side note - make sure to set the sigcontext's CS register variable
to the correct value. Automation like pwntools will do this for you
automatically. Failing to do so will result in crashing the target
process. Several of the examples below explicitly set the CS value.

## The original concept

The original concept of SROP was introduced in 2014 by Erik Bosman and
Herbert Bos in their "Framing Signals - A Return to Portable Shellcode"
paper. This document explains the theory and practice.

"Framing Signals - A Return to Portable Shellcode" - Erik Bosman, Herbert Bos
- https://www.cs.vu.nl/~herbertb/papers/srop_sp14.pdf
- https://ieeexplore.ieee.org/document/6956568

## A thorough example

Mehdi Talbi explores how Unix signals work. They then write an example
x86 64-bit application and demonstrate how to exploit it using SROP.

"Playing with signals: An overview on sigreturn oriented programming" -
Mehdi Talbi
- https://mtalbi.github.io/exploit,/sigreturn/oriented/programming/2015/01/03/playing-with-signals.html

## Using SROP to store and execute shellcode via the .text section

Reno Robert wrote a very short blog post demonstrating how SROP can be
used to make a x86 32-bit process's .text section writable and executable.
They then point the stack pointer to the .text section and write shellcode
to the new "stack" (i.e., the .text section).

"Fun with SROP Exploitation" - Reno Robert
- https://www.voidsecurity.in/2015/06/fun-with-srop-exploitation.html

## A very brief example

Oussama Amri's blog post is conceptually similar to Robert's (the previous
blog post). However, they use a x86 64-bit program as an example.

"Sigreturn-Oriented Programming (SROP)" - Oussama Amri
- https://amriunix.com/posts/sigreturn-oriented-programming-srop/
