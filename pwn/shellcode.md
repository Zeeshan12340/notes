# shellcode
```text-plain
.globl _start
_start:
.intel_syntax noprefix
        mov rax, 59				# syscall number for execve
        lea rdi, [rip+binsh]	# first arg of execve "/bin/sh"
        mov rsi, 0				# second arg, argv, NULL
        mov rdx, 0				# third arg, envp, NULL
        syscall					# trigger syscall
binsh:
        .string "/bin/sh" 
```

*   `LEA` means Load Effective Address
*   `MOV` means Load Value

In short, `LEA` loads a pointer to the item you're addressing whereas MOV loads the actual value at that address.

The purpose of `LEA` is to allow one to perform a non-trivial address calculation and store the result \[for later usage\]

```text-plain
LEA ax, [BP+SI+5] ; Compute address of value

MOV ax, [BP+SI+5] ; Load value at that address
```

[https://filippo.io/linux-syscall-table/](https://filippo.io/linux-syscall-table/) 

[https://blog.skullsecurity.org/2021/bsidessf-ctf-2021-author-writeup-shellcode-primer-runme-runme2-and-runme3](https://blog.skullsecurity.org/2021/bsidessf-ctf-2021-author-writeup-shellcode-primer-runme-runme2-and-runme3)