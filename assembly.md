# Assembly (asm) notes
Various notes about reading and writing assembly (mostly Intel x86[/64]).

#### Writing and compiling assembly with `nasm`
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

Compile to ELF32 (Executable and Linkable Format):
```
nasm shell_32.asm -f elf32
ld shell_32.o shell_32 -m elf_i386
```

Compile to binary:
```
nasm shell_32.asm -f bin
```
