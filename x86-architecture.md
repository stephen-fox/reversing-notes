# x86 CPU architecture

Notes about x86 CPU architecture and design.

## Addressing mode terminology

The following example is based on this stackoverflow question and answer by
Future Gadget and Peter Cordes:

- https://stackoverflow.com/questions/52564064/difference-betwen-base-and-displacement

```asm
;                         + offset (here, the result of math in brackets)
;                         |
;                  |-------------|
imul eax,DWORD PTR [esi+ebx*4-0x4]
;                   |   |---| |
;                   |     |   + displacement
;                   |     |
;                   |     + index (here, "scaled index")
;                   |
;                   + base index (optional)
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
