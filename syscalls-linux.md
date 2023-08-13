# Linux system calls notes

## Finding system call number

https://stackoverflow.com/a/53123818 by Gil Hamilton

```sh
find /usr/include/ -name 'unistd*.h'
# ...
/usr/include/x86_64-linux-gnu/asm/unistd_64.h
#...
grep 'execveat' /usr/include/x86_64-linux-gnu/asm/unistd_64.h
#
# Can also use strace source code:
# https://github.com/strace/strace/blob/v4.26/linux/i386/syscallent.h
```
