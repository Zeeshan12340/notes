# gdb
we can debug asm binaries the same way, to update the value of a register use, `set $rdi = 0x12345`, or to write to a referenced memory location we can use:

```text-plain
set {int}0x400000 = 0x7f454c46
set $rdi = 0x400000
```