# sub register table
|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |
| **Name** | **Notes** | Type | **64-bit**  <br>**long** | **32-bit**  <br>**int** | **16-bit**  <br>**short** | **8-bit**  <br>**char** |
| rax | Values are returned from functions in this register. | scratch | rax | eax | ax  | ah and al |
| rcx | Typical scratch register.  Some instructions also use it as a counter. | scratch | rcx | ecx | cx  | ch and cl |
| rdx | Scratch register. | scratch | rdx | edx | dx  | dh and dl |
| _rbx_ | _Preserved register: don't use it without saving it!_ | _preserved_ | _rbx_ | _ebx_ | _bx_ | _bh and bl_ |
| _rsp_ | _The stack pointer.  Points to the top of the stack (details coming soon!)_ | _preserved_ | _rsp_ | _esp_ | _sp_ | _spl_ |
| _rbp_ | _Preserved register.  Sometimes used to store the old value of the stack pointer, or the "base"._ | _preserved_ | _rbp_ | _ebp_ | _bp_ | _bpl_ |
| rsi | Scratch register.  Also used to pass function argument #2 in 64-bit Linux | scratch | rsi | esi | si  | sil |
| rdi | Scratch register.  Function argument #1 in 64-bit Linux | scratch | rdi | edi | di  | dil |
| r8  | Scratch register.  These were added in 64-bit mode, so they have numbers, not names. | scratch | r8  | r8d | r8w | r8b |
| r9  | Scratch register. | scratch | r9  | r9d | r9w | r9b |
| r10 | Scratch register. | scratch | r10 | r10d | r10w | r10b |
| r11 | Scratch register. | scratch | r11 | r11d | r11w | r11b |
| _r12_ | _Preserved register.  You can use it, but you need to save and restore it._ | _preserved_ | _r12_ | _r12d_ | _r12w_ | _r12b_ |
| _r13_ | _Preserved register._ | _preserved_ | _r13_ | _r13d_ | _r13w_ | _r13b_ |
| _r14_ | _Preserved register._ | _preserved_ | _r14_ | _r14d_ | _r14w_ | _r14b_ |
| _r15_ | _Preserved register._ | _preserved_ | _r15_ | _r15d_ | _r15w_ | _r15b_ |