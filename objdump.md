# objdump notes
Notes about the objdump dissassembly tool.

## Dissassemble a program
```
objdump -d vuln
 80490d2:	5e                   	pop    %esi
 80490f5:	56                   	push   %esi
 8049157:	8d b4 26 00 00 00 00 	lea    0x0(%esi,%eiz,1),%esi
 8049161:	8d b4 26 00 00 00 00 	lea    0x0(%esi,%eiz,1),%esi
 8049168:	8d b4 26 00 00 00 00 	lea    0x0(%esi,%eiz,1),%esi
 80491a4:	8d 74 26 00          	lea    0x0(%esi,%eiz,1),%esi
 80491a9:	8d b4 26 00 00 00 00 	lea    0x0(%esi,%eiz,1),%esi
 80491cd:	8d 76 00             	lea    0x0(%esi),%esi
 80491d1:	8d b4 26 00 00 00 00 	lea    0x0(%esi,%eiz,1),%esi
 80491d8:	8d b4 26 00 00 00 00 	lea    0x0(%esi,%eiz,1),%esi
 804933d:	56                   	push   %esi
 8049360:	31 f6                	xor    %esi,%esi
 8049362:	8d b6 00 00 00 00    	lea    0x0(%esi),%esi
 8049374:	ff 94 b5 08 ff ff ff 	call   *-0xf8(%ebp,%esi,4)
 804937b:	83 c6 01             	add    $0x1,%esi
 8049381:	39 f3                	cmp    %esi,%ebx
 8049389:	5e                   	pop    %esi
 804938d:	8d 76 00             	lea    0x0(%esi),%esi
```

## Disassemble raw binary
https://stackoverflow.com/a/34424194
```
objdump -D -M intel,x86-64 -b binary -m i386 foo.bin
foo.bin:     file format binary


Disassembly of section .data:

00000000 <.data>:
   0:	ba dc fe 21 43       	mov    edx,0x4321fedc
   5:	be 69 19 12 28       	mov    esi,0x28121969
   a:	bf ad de e1 fe       	mov    edi,0xfee1dead
   f:	b0 a9                	mov    al,0xa9
  11:	0f 05                	syscall 
```
