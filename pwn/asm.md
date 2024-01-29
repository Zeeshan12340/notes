# asm
```text-plain
.globl _start
_start:
.intel_syntax noprefix
        mov rdi, 0x1337
```

boiler plate asm code, compile with `gcc -nostdlib -static -o rdi rdi.s`. Passing the entirety of this binary into the challenge program errors out, we onlly need the `.text`  section, extract it with `objcopy --dump-section .text=rdi_text rdi`

The relevant instructions for this level are:  
`mov rax, reg1; div reg2`  
Notice: to use this instruction you need to first load rax with the desired register you intended to be the divided. Then run `div reg2` where reg2 is the divisor. This results in:  
`rax = rdi / rsi; rdx = remainder`  
The quotient is placed in rax, the remainder is placed in rdx.

for modulus with power 2 numbers we can just move the least significant bits from our registers, as 256, 65536 translate to 100, 10000 in hex, so the remainder after division(modulo) is just the last bits in the original values/registers.

`mov al, dil` , `mov bx, si`

mov rax, \[some\_address\]        <=>     Moves the thing at 'some\_address' into rax  
This also works with things in registers:  
mov rax, \[rdi\]         <=>     Moves the thing stored at the address of what rdi holds to rax

This works the same for writing:  
mov \[rax\], rdi         <=>     Moves rdi to the address of what rax holds.

So if rax was 0xdeadbeef, then rdi would get stored at the address 0xdeadbeef(rather than in rax) :  
\[0xdeadbeef\] = rdi  
Note: memory is linear, and in x86, it goes from 0 - 0xffffffffffffffff (yes, huge).

\* Quad Word = 8 Bytes = 64 bits  
\* Double Word = 4 bytes = 32 bits  
\* Word = 2 bytes = 16 bits  
\* Byte = 1 byte = 8 bits

we cannot mov 64 bit values directly into de-referenced memory locations, first mov the value into a temporary register and then mov from that register into the memory address.

`jmp $+0x53` for jumping to an offset of your current location, also `.` is "the current position" (the start of this instruction)

offsets in memory locations can directly referenced with instructions such as: `add rax, [rdi+8*rcx]`

### loops in assembly

`.rept 0x53; nop; .endr` repeat 0x53 times the instruction `nop` and then end

### functions

Use `call` in order to call the function and `ret` to return from the function.

What occurs when you type `call` is that the address of the next instruction is `push`ed into the stack. When `ret` is hit, it will `pop` that address off the stack and `jmp` to it.

```text-plain
func:
    xor eax, eax
    mov eax, 10
    add eax, 5
    ret ;// essentially identical to: pop [register] -> jmp [register]


_start:
    call func
    mov ebx, eax ;// Address of this instruction is pushed onto the stack
    ;// ebx is now 15
```

Calling convention dictates that the `EAX` register should contain the return value. Also note that the [\_\_cdecl calling convention](https://en.wikibooks.org/wiki/X86_Disassembly/Calling_Conventions#CDECL) takes parameters on the stack. Take a look at the examples in the afore-linked page. The NASM function will set up its stack frame and take parameters from the stack in order to use in the function. The value is stored in `EAX`.

Stack interaction:
------------------

this loads 23 into rax, and then 17 into rcx:

push 17  
push 23  
pop rax  
pop rcx  
ret

After the first "push", the stack just has one value:  
    17  
After the second "push", the stack has two values:  
    17  23  
So the first "pop" picks up the 23, and puts it in rax, leaving the stack with one value:  
    17  
The second "pop" picks up that value, puts it in rcx, leaving the stack clean. 

The "call" instruction pushes the memory address of the next instruction onto the stack and then jumps to the value stored in the first argument.

Let's use the following instructions as an example:

```text-plain
0x1021 mov rax, 0x400000
0x1028 call rax
0x102a mov [rsi], rax
```

1\. call pushes 0x102a, the address of the next instruction, onto the stack.  
2\. call jumps to 0x400000, the value stored in rax.  
The "ret" instruction is the opposite of "call". ret pops the top value off of  
the stack and jumps to it.

Stack frame:
------------

 A function stack frame is a set of pointers and values pushed onto the stack to save things for later use and allocate space on the stack for function variables.

`rbp`, the Stack Base Pointer. The rbp register is used to tell where our stack frame first started.

As an example, say we want to construct some list (a contigous space of memory) that is only used in our function. The list is 5 elements long, each element is a dword. A list of 5 elements would already take 5 registers, so instead, we can make pace on the stack! The assembly would look like:

* * *

```text-plain
; setup the base of the stack as the current top
mov rbp, rsp

; move the stack 0x14 bytes (5 * 4) down
; acts as an allocation
sub rsp, 0x14

; assign list[2] = 1337
mov eax, 1337
mov [rbp-0x8], eax
; do more operations on the list ...

; restore the allocated space
mov rsp, rbp
ret
```

* * *

Notice how rbp is always used to restore the stack to where it originally was. If we don't restore the stack after use, we will eventually run out. Moreover notice how we subtracted from `rsp` since the stack grows down. To make it have more space, we subtract the space we need. The ret and call still works the same. It is assumed that you will never pass a stack address across functions, since, as you can see from the above use, the stack can be overwritten by anyone at any time.

A system-call is done via the syscall instruction. The kernel destroys registers %rcx and %r11.