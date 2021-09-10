# General command line / shell notes
Various notes on helpful command line and shell-isms.

## Reading a file into a program and keeping stdin open
Helpful when working with an exploitable program that reads from stdin.

```sh
# https://security.stackexchange.com/a/120501
cat shellcode.hex - | ./vulnerable_program
```

## Hooking a program's std file descriptors up to another program in Bash
```sh
# https://stackoverflow.com/a/36327396
#!/bin/bash

coproc myapp
nc -kl -p 4000 <&"${COPROC[0]}" >&"${COPROC[1]}"
```

## Printing a character n times
```sh
# https://stackoverflow.com/a/17030976
printf "%0.sA" {1..10}
```

## Making '/bin/sh' reverse shell more usable
```sh
# Note these commands are executed in the reverse shell.
script /dev/null
# Note: There are probably alternatives to python.
python -c 'import pty;pty.spawn("/bin/bash");'
# Press Ctrl+Z.
stty raw -echo
fg
# Press enter a few times.
# Now you can execute 'bash -i' or other things.
# Setting the 'XTERM=xterm' env. can be helpful for 'top' and other things too.
```
