# rizin

## Searching for bytes

Note: The rizin documentation for this appears to be missing / half complete.
The radare2 documentation can be used in place of it:

- https://book.rada.re/search_bytes/intro.html

#### List available memory search area(s)

```
e search.in=?
```

#### Set memory search area

```
# This one seems useful in the debugger:
e search.in=dbg.maps.rw
```

#### Search for a hex-encoded value in `e search.in`

```
/x 2e6b792cca055bf6de539d17a5c67dcb75d360ea
```
