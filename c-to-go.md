# Converting C to Go

These notes cover converting C code to Go, mainly for the purposes of
recreating libc structs in Go.

## Converting `_IO_FILE` to a Go struct

1. Install Go
2. Install cxgo:
   - `go install github.com/gotranspile/cxgo/cmd/cxgo@latest`
3. Clone or download the glibc source code:
   - Download:
     1. `curl -LO https://ftp.gnu.org/gnu/glibc/glibc-2.39.tar.gz`
     2. `tar -xzf glibc-2.39.tar.gz`
   - Clone:
     - `git clone https://sourceware.org/git/glibc.git`
4. Set various things in header files:

```sh
sed -i '' 's|^#error|//&|' glibc-2.39/bits/wordsize.h
sed -i '' 's|^#define __WORDSIZE$|& 64|' glibc-2.39/bits/wordsize.h
sed -i '' 's|^#include_next <features-time64.h>$|//&|' glibc-2.39/include/features-time64.h
```

5. Create the following cxgo config file (named `glibc-fileobj-cxgo.yaml`)

```yaml
root: glibc-2.39
out: glibc-fileobj-go
package: glibc
include: ['.']
sys_include: ['.']
define:
- name: POSIX
  value: "1"
# _ISOMAC gets us to skip code in "include/sys/cdefs.h"
# that makes cxgo unhappy.
- name: _ISOMAC
  value: "1"
# Note: It seems like this define does not work :(
- name: __WORDSIZE
  value: "64"
replace:
  - old: '*byte'
    new: 'uint64 // *byte'
  - old: '__off64_t'
    new: 'uint64 // __off64_t'
  - old: 'size_t'
    new: 'uint64 // size_t'
  - old: '__off_t'
    new: 'uint64 // __off_t'
  - old: '*_IO_codecvt'
    new: 'uint64 // *_IO_codecvt'
  - old: '*_IO_wide_data'
    new: 'uint64 // *_IO_wide_data'
  - old: '*_IO_FILE'
    new: 'uint64 // *_IO_FILE'
  - old: '*_IO_marker'
    new: 'uint64 // *_IO_marker'
  - old: 'unsafe.Pointer'
    new: 'uint64 // unsafe.Pointer'
  - old: 'import "unsafe"'
    new: ''
files:
  - name: libio/bits/types/struct_FILE.h
```

6. Run cxgo:
   - `cxgo -c glibc-fileobj-cxgo.yaml`
