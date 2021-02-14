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
