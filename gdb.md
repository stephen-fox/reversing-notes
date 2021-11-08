# gdb notes

## Debug a not-yet-started program
```sh
gdb path-to-program
# At the gdb prompt:
r
# Or run with arguments.
r arg1 arg2 argN
```
## Set maximum number of lines per command
```sh
set listsize 200
```

## Print out source code
```sh
list
```

## Add breakpoint for source file at line number
```sh
b main.c:22
```

## Delete a breakpoint by its number
```sh
delete 1
```

## List breakpoints
```sh
info breakpoints
```

## Step over a single CPU instruction
```sh
si
```

## Step over n CPU instructions
```sh
si 2
```

## Print all variables
```sh
info variables
All defined variables:
# (...)
```

## Filter variables and print them
```sh
info variables malloc
All variables matching regular expression "malloc":
# (...)
```

## Print information about a variable
```sh
info address __malloc_hook 
Symbol "__malloc_hook" is static storage at address 0x7fba7a49db70.
```

## Set a variable's value by name
```sh
set variable __malloc_hook  = 0x7fba7a327e50
```

## Set pointer at memory address
```sh
set {int} 0x7fba7a49db7000 = 0xf00f00f00f000
# Or provide a pointer by variable name, such as the pointer to 'system()'::
set {int} 0x7fba7a49db7000 = system
```

## Write a string to a memory address
```sh
set {char [8]} 0x7ffeee19dcf4 = "/bin/sh"
```

## Print 4 bytes at address
```sh
x/x 0x7fba7a49db70
0x7fba7a49db70 <__malloc_hook>:	0x497aba7f
```

## Print 8 bytes at address
```sh
x/2x 0x7fba7a49db70
0x7fba7a49db70 <__malloc_hook>:	0x497aba7f	0x00007fba
```

## Print address pointed to by another address
```sh
p/a *0x7fba7a49db70
$25 = 0xf00f000
```

## Print a function's PLT address
```sh
info functions printf@plt
All functions matching regular expression "printf@plt":

Non-debugging symbols:
0x0000564d2264c090  printf@plt
```

## Calculate offset between symbols
```sh
print system - __libc_start_main+247
```

## Print a function's address
```sh
print system
$8 = {int (const char *)} 0x7fba7a327e50 <__libc_system>
```

## Print registers' values
```sh
info registers 
rax            0x0                 0
rbx            0x0                 0
# (...)
```

## Print some of the stack
```sh
x/100x $rsp
```

## Print memory mappings
```sh
info proc mappings
process 66775
Mapped address spaces:

          Start Addr           End Addr       Size     Offset objfile
      0x55cf3fde4000     0x55cf3fde5000     0x1000        0x0 /foo
# (...)
      0x7f26b8a66000     0x7f26b8a8b000    0x25000        0x0 /usr/lib/x86_64-linux-gnu/libc-2.31.so
# (...)
```

## Set breakpoint at a memory address
```sh
b *0xf00f00
```

## Follow child processes
```sh
set follow-fork-mode child
```
