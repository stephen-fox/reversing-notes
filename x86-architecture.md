# x86 CPU architecture

Notes about x86 CPU architecture and design.

## Addressing mode terminology

This write up by Sivarama P. Dandamudi provides an excellent overview of
x86 addressing:

- https://people.scs.carleton.ca/~sivarama/asm_book_web/Student_copies/ch5_addrmodes.pdf

The following example is based on this stackoverflow question and answer by
Future Gadget and Peter Cordes:

- https://stackoverflow.com/questions/52564064/difference-betwen-base-and-displacement

```asm
;                          + offset (i.e., the result of math in brackets)
;                          |
;                   |-------------|
imul eax, DWORD PTR [esi+ebx*4-0x4]
;                    |   |   | |
;                    |   |   | + displacement (optional)
;                    |   |   |
;                    |   |   + scale (optional)
;                    |   |
;                    |   + index (here, "scaled index")
;                    |
;                    + base (optional)
;
; What actually happens here:
;
; 1. ebx * 4
; 2. esi + the result of operation 1
; 3. substract 4 from the result
; 4. go to the address (result) and get the value inside it.
```

## x86 16 byte call stack alignment

x86 CPUs align call stack memory on a 16 byte boundary.

```asm
; if esp == 0x7fAABBCC, then esp == 0x7FAABBC0
and esp, 0xfffffff0
```

- https://stackoverflow.com/questions/28472455/what-is-and-esp-0xfffffff0

## Returning a value

`eax` (or `rax` on 64-bit) is used to store the return value.

- https://stackoverflow.com/questions/55773868/returning-a-value-in-x86-assembly-language

## Jumps

Stackoverflow user zx485 wrote this super helpful lookup table for x86 jumps
here: https://stackoverflow.com/a/53452319

```
Mnemonic        Condition tested       Description
jo              OF = 1                 overflow
jno             OF = 0                 not overflow
jc, jb, jnae    CF = 1                 carry / below / not above nor equal
jnc, jae, jnb   CF = 0                 not carry / above or equal / not below
je, jz          ZF = 1                 equal / zero
jne, jnz        ZF = 0                 not equal / not zero
jbe, jna        CF or ZF = 1           below or equal / not above
ja, jnbe        CF or ZF = 0           above / not below or equal
js              SF = 1                 sign
jns             SF = 0                 not sign
jp, jpe         PF = 1                 parity / parity even
jnp, jpo        PF = 0                 not parity / parity odd
jl, jnge        SF xor OF = 1          less / not greater nor equal
jge, jnl        SF xor OF = 0          greater or equal / not less
jle, jng        (SF xor OF) or ZF = 1  less or equal / not greater
jg, jnle        (SF xor OF) or ZF = 0  greater / not less nor equal
```
