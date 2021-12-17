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

## Overriding Bash builtins with environment variables

```sh
# Note: "export" does not like this syntax; you need to find another way to
# set the environment variable through a parent process.
# The following example overrides "echo" to call "/bin/echo" with a prefix:
BASH_FUNC_echo%%='() { /bin/echo "w00t $@"; }'
```

## Execute a program each time a Bash prompt is written

```sh
export PROMPT_COMMAND="echo foo"
```

## Source / execute a shell script when a new Bash shell is started

```sh
# This example executes "/path/to/my/script.sh" when a new Bash shell starts.
export BASH_ENV=/path/to/my/script.sh
bash
```

## Shell command injection without spaces
"Command injection without spaces", fyoorer
- https://www.betterhacker.com/2016/10/command-injection-without-spaces.html

```sh
# Bash:
{echo,foo.bar}
# Other shells:
args=$'\x20/etc/passwd'
cat$args
```
