# pwntools notes
Python is the best.

See https://docs.pwntools.com/en/latest/intro.html#tutorials for more.

## Python setup
```sh
sudo apt install -y python3-venv
sudo apt install python3-pip
```

## Project setup
```sh
# Note: Be careful about conflicting names (i.e., calling the project 'pwn' will
# conflict with the pwntools 'pwn' namespace).
mkdir foo
cd foo
python3 -m venv bar
source bar/bin/activate
pip3 install pwntools
pip freeze > requirements.txt
vi foo.py
```

## Python file example
```python
#!/usr/bin/env python3

from pwn import *
```

## Correcting Python 2 assumptions

### Strings versus bytes
Many pwntools examples assume Python 2 (because it is the best). As such, you
will see code like the following:

```python
from pwn import *

payload  = "exit".ljust(8)
payload += "|%16$p|".rjust(8)
payload += p64(0x601258)
```

This is invalid in Python 3 because `payload` is assumed to be a `string`. The
author intended `payload` to be `bytes`, as such the `p64(...)` concatenation is
invalid (as it returns bytes, not a string). The solution is to convert any
strings to bytes using `b"foo"`. Applying this to the snippet above results in
the following:

```python
from pwn import *

payload  = b"exit".ljust(8)
payload += b"|%16$p|".rjust(8)
payload += p64(0x601258)
```

This converts any strings to bytes before concatenating them together, thus
avoiding the type error.

## Finger printing local libc
Here is some awesome code.

```python
#!/usr/bin/env python3

from pwn import *
import sys

if len(sys.argv) == 1:
    sys.stderr.write("please specify at least one libc function to lookup\n")
    exit(1)

# TODO: Hardcoded.
libc=ELF("/lib/x86_64-linux-gnu/libc.so.6")

for arg in sys.argv[1:]:
    print(arg, hex(libc.symbols[arg])
```
