# radare2 notes

## Get the state of common CPU registers
```
dr
eax = 0x00000000
ebx = 0x00000000
ecx = 0x00000000
edx = 0x00000000
esi = 0x00000000
edi = 0x00000000
esp = 0xffda6e30
ebp = 0x00000000
eip = 0xf7f920b0
eflags = 0x00000200
oeax = 0x0000000b
```

## Get the state of the specified register (esp)
```
dr esp
0xffcaf310
```

## Get the state of all CPU registers
```
drt all
eax = 0x00000000
ax = 0x00000000
ah = 0x00000000
al = 0x00000000
ebx = 0x00000000
bx = 0x00000000
bh = 0x00000000
bl = 0x00000000
ecx = 0x00000000
cx = 0x00000000
ch = 0x00000000
cl = 0x00000000
# Snip.
xmm5h = 0x00000000
xmm5l = 0x00000000
xmm6h = 0x00000000
xmm6l = 0x00000000
xmm7h = 0x00000000
xmm7l = 0x00000000
x64-32 = 0x00000000
```

## Show words with references to flags and code at the specified address
```
pxr @ esp
0xffa05b28 0x00000040  @... @esp 64 (.symtab) ascii ('@')
0xffa05b2c 0x083031b0  .10. ([heap]) heap R W X 'mov byte [ebp*4 + 0xfb], ah' '[heap]'
0xffa05b30 0x080491ee  .... (/home/kali/Desktop/vuln) (.text) sym.flag program R X 'add ebx, 0x2e12' 'vuln'
0xffa05b34 0xf3295435  5T).
0xffa05b38 0xb68ebc8b  ....
0xffa05b3c 0xa6d0fbf3  ....
0xffa05b40 0x2559fbfb  ..Y%
0xffa05b44 0x6b55103a  :.Uk
0xffa05b48 0x16d5eb5e  ^...
0xffa05b4c 0x2990746c  lt.)
0xffa05b50 0x20c16516  .e. 
0xffa05b54 0x16471c06  ..G.
0xffa05b58 0xd76a1c79  y.j.
0xffa05b5c 0xda0ce3fc  ....
0xffa05b60 0xdb540201  ..T.
0xffa05b64 0x67a4c5fd  ...g
0xffa05b68 0x97a4c5fc  ....
0xffa05b6c 0x41414532  2EAA ascii ('2')
```

## Get hexadecimal representation of data starting at address (ebp - 200 bytes)
```
pxw @ ebp-200
0x0804bf38  0x0000001a 0x0804bf0c 0x0000001c 0x00000004  ................
0x0804bf48  0x6ffffef5 0x080481ec 0x00000005 0x080482ec  ...o............
0x0804bf58  0x00000006 0x0804820c 0x0000000a 0x0000008d  ................
0x0804bf68  0x0000000b 0x00000010 0x00000015 0xf7f42928  ............()..
0x0804bf78  0x00000003 0x0804c000 0x00000002 0x00000050  ............P...
0x0804bf88  0x00000014 0x00000011 0x00000017 0x080483d8  ................
0x0804bf98  0x00000011 0x080483c8 0x00000012 0x00000010  ................
0x0804bfa8  0x00000013 0x00000008 0x6ffffffe 0x08048398  ...........o....
0x0804bfb8  0x6fffffff 0x00000001 0x6ffffff0 0x0804837a  ...o.......oz...
0x0804bfc8  0x00000000 0x00000000 0x00000000 0x00000000  ................
0x0804bfd8  0x00000000 0x00000000 0x00000000 0x00000000  ................
0x0804bfe8  0x00000000 0x00000000 0x00000000 0x00000000  ................
0x0804bff8  0x00000000 0xf7ef8dbc 0x0804bf10 0xf7f42940  ............@)..
0x0804c008  0xf7f2e2b0 0x08049036 0x08049046 0x08049056  ....6...F...V...
0x0804c018  0x08049066 0x08049076 0x08049086 0xf7d36e00  f...v........n..
0x0804c028  0x080490a6 0x080490b6 0x080490c6 0x00000000  ................
```

## Dissassemble and print n (10) instructions
```
pd 10
│           ;-- eip:
│           0x08049235 b    ff75f4         push dword [var_ch]
│           0x08049238      6a40           push 0x40                   ; '@' ; 64
│           0x0804923a b    8d45b4         lea eax, dword [var_4ch]
│           0x0804923d      50             push eax
│           0x0804923e      e80dfeffff     call sym.imp.fgets          ; char *fgets(char *s, int size, FILE *stream)
│           0x08049243      83c410         add esp, 0x10
│           0x08049246      817d08efbead.  cmp dword [arg_8h], 0xdeadbeef
│       ┌─< 0x0804924d      751a           jne 0x8049269
│       │   0x0804924f      817d0c0dd0de.  cmp dword [arg_ch], 0xc0ded00d
│      ┌──< 0x08049256      7514           jne 0x804926c
```

## List the address of a function (system) for the specified library (libc)
```
dmi libc system
257   0x00131c30 0xf7e68c30 GLOBAL FUNC   102      svcerr_systemerr
661   0x00044620 0xf7d7b620 GLOBAL FUNC   55       __libc_system
1533  0x00044620 0xf7d7b620 WEAK   FUNC   55       system
```

## Get information about the current binary's sections
```
iS
[Sections]

nth paddr        size vaddr       vsize perm name
―――――――――――――――――――――――――――――――――――――――――――――――――
0   0x00000000    0x0 0x00000000    0x0 ---- 
1   0x00000194   0x13 0x08048194   0x13 -r-- .interp
2   0x000001a8   0x24 0x080481a8   0x24 -r-- .note.gnu.build_id
3   0x000001cc   0x20 0x080481cc   0x20 -r-- .note.ABI_tag
4   0x000001ec   0x20 0x080481ec   0x20 -r-- .gnu.hash
5   0x0000020c   0xe0 0x0804820c   0xe0 -r-- .dynsym
6   0x000002ec   0x8d 0x080482ec   0x8d -r-- .dynstr
7   0x0000037a   0x1c 0x0804837a   0x1c -r-- .gnu.version
8   0x00000398   0x30 0x08048398   0x30 -r-- .gnu.version_r
9   0x000003c8   0x10 0x080483c8   0x10 -r-- .rel.dyn
10  0x000003d8   0x50 0x080483d8   0x50 -r-- .rel.plt
11  0x00001000   0x20 0x08049000   0x20 -r-x .init
12  0x00001020   0xb0 0x08049020   0xb0 -r-x .plt
13  0x000010d0  0x2c5 0x080490d0  0x2c5 -r-x .text
14  0x00001398   0x14 0x08049398   0x14 -r-x .fini
15  0x00002000   0x55 0x0804a000   0x55 -r-- .rodata
16  0x00002058   0x54 0x0804a058   0x54 -r-- .eh_frame_hdr
17  0x000020ac  0x170 0x0804a0ac  0x170 -r-- .eh_frame
18  0x00002f08    0x4 0x0804bf08    0x4 -rw- .init_array
19  0x00002f0c    0x4 0x0804bf0c    0x4 -rw- .fini_array
20  0x00002f10   0xe8 0x0804bf10   0xe8 -rw- .dynamic
21  0x00002ff8    0x8 0x0804bff8    0x8 -rw- .got
22  0x00003000   0x34 0x0804c000   0x34 -rw- .got.plt
23  0x00003034    0x8 0x0804c034    0x8 -rw- .data
24  0x0000303c    0x0 0x0804c03c    0x4 -rw- .bss
25  0x0000303c   0x1d 0x00000000   0x1d ---- .comment
26  0x0000305c  0x4b0 0x00000000  0x4b0 ---- .symtab
27  0x0000350c  0x292 0x00000000  0x292 ---- .strtab
28  0x0000379e  0x101 0x00000000  0x101 ---- .shstrtab
```

## Print the values of the current function's arguments and variables
```
afvd
var var_b8h = 0x41304178 = -1
var var_4h = 0x4130422c = -1
```

## Search for instuctions with specified operands
```
/am call eax
```

## Search for operations on a register
```
/ad esi
```

## Write a string ('foo') to an address (0x0804c03c)
```
w foo @ 0x0804c03c
```
## Rewrite the value of a registera
```
dr eax = 0xdeadbeef
```
