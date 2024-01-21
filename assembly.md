# Assembly (asm) notes

Various notes about reading and writing assembly (mostly Intel x86[/64]).

## Syntax

#### Brackets

Brackets indicate pointer de-reference. For example, `mov ebx, dword [esp]`
means copy what `esp` points to into `ebx`. If the value of `esp` were a valid
memory pointer, and it pointed to the value `0x04`, then the `ebx` register
value would become `0x04`.

## Writing and compiling assembly with `nasm`

- Writing '/bin/sh' asm: https://security.stackexchange.com/a/191387
- Compiling to binary: https://stackoverflow.com/a/8482487

Example: `shell_32.asm`

```asm
section .data

str: db "/bin/sh", 0x00

section .text
        global _start

_start: 
        xor eax, eax
        xor ebx, ebx
        xor ecx, ecx
        xor edx, edx
        mov eax, 11
        mov ebx, str
        mov ecx, 0
        mov edx, 0
        int 0x80
```

Or a [64-bit example](https://stackoverflow.com/a/42750204) by "int80":

```asm
section .data
file db '/bin/sh',0
file_arg db 'sh',0
argv dq file_arg, 0

section .text
global _start
_start:
mov     rax, 59
mov     rdi, file
mov     rsi, argv
mov     rdx, 0
syscall
```

#### Compile to ELF32 (Executable and Linkable Format):

```sh
nasm src.asm -f elf32
ld src.o -m elf_i386
```

#### Compile to ELF64

```sh
nasm src.asm -f elf64
ld src.o -m elf_x86_64
```

#### Compile to binary:

```sh
nasm src.asm -f bin
```

## Overview of Intel x86 assembly registers and instructions

"x86 Assembly Guide", Quentin Carbonneaux
- http://flint.cs.yale.edu/cs421/papers/x86-asm/asm.html

## `popal` x86 instruction

"Pop All General-Purpose Registers",
- https://c9x.me/x86/html/file_module_x86_id_249.html

Observations:

Consumes 36 bytes (9 dwords) from the stack:
```
[0: edi] [1: esi] [2: ebp] [3: ?] [4: ebx] [5: edx] [6: ecx] [7: eax] [8: eip]
```

## Relative jumps in Intel x86

"Using SHORT (Two-byte) Relative Jump Instructions", Daniel B. Sedory
- https://thestarman.pcministry.com/asm/2bytejumps.htm
