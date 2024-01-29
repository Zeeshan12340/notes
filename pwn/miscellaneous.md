# miscellaneous
file descriptors in bash work something like this:

```text-plain
exec 50<> stdin #where 50 is the file descriptor shown /proc/self/fd and stdin is a named pipe
urowajyz
```