# shell stablization
First, follow the same technique as in Method 1 and use Python to spawn a PTY. Once bash is running in the PTY, background the shell with `Ctrl-Z`

`python -c 'import pty; pty.spawn("/bin/bash")'`

With the shell still backgrounded, now set the current STTY to type raw and tell it to echo the input characters with the following command:

`stty raw -echo`

With a raw stty, input/output will look weird and you won’t see the next commands, but as you type they are being processed.

Next foreground the shell with `fg`. It will re-open the reverse shell but formatting will be off. Finally, reinitialize the terminal with `reset`.

After the `reset` the shell should look normal again. The last step is to set the shell, terminal type and stty size to match our current Kali window (from the info gathered above)

|     |     |
| --- | --- |
| ```text-plain<br>1<br>2<br>3<br>``` | ```text-plain<br>$ export SHELL=bash<br>$ export TERM=xterm256-color<br>$ stty rows 38 columns 116<br>``` |