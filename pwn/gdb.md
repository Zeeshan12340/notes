# gdb
You can use the command `start` to start a program, with a breakpoint set on `main`. 

You can use the command `starti` to start a program, with a breakpoint set on `_start`. You can use the command `attach <PID>` to attach to some other already running program. You can use the command `core <PATH>` to analyze the coredump of an already run program.

You can examine the contents of memory using the `x/<n><u><f> <address>` parameterized command. In this format `<u>` is the unit size to display, `<f>` is the format to display it in, and `<n>` is the number of elements to display. Valid unit sizes are `b` (1 byte), `h` (2  ytes), `w` (4 bytes), and `g` (8 bytes). Valid formats are `d` (decimal), `x` (hexadecimal), `s` (string) and `i` (instruction). The address can be specified using a register name, symbol name, or absolute address. Additionally, you can supply mathematical expressions when specifying the address.

You will probably want to view your instructions using the CORRECT assembly syntax. You can do that with the command 

`set disassembly-flavor intel`

You can use the `finish` command in order to finish the currently executing function.

If you know how to interact with gdb, you already know how to write a gdb script--the syntax is exactly the same. You can write your commands to some file, for example `x.gdb`, and then launch gdb using the flag `-x <PATH_TO_SCRIPT>`.

You can use `set *((uint64_t *) $rsp) = 0x1234` to set the first value on the stack to 0x1234. You can use `set *((uint16_t *) 0x31337000) = 0x1337` to set 2 bytes at 0x31337000 to 0x1337.

`call (void)win()` to call any specific function