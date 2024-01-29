# calling problems
```text-plain
.globl _start
_start:
.intel_syntax noprefix
        mov rbx, 0x61 
        push rbx

        push rsp
        pop rdi
        
        push 7
        pop rsi
        
        mov al, 90
        syscall
```

here, `push rsp` is weird, but it's critical. If I just push the hex value 0x61("a") into rdi from rbx, the function call errors out with invalid address, so we need a pointer to our value/address, the first `push rbx` pushes the value on the stack and the second push pushes the pointer to that address(rsp) on the stack which can be used with function calls. We then pop that value for use with our function.

![](calling%20problems/image.png)