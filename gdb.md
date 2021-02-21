# gdb notes

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

## Set value at memory address
```sh
set {int}0x7fba7a49db7000=0xf00f00f00f000
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
