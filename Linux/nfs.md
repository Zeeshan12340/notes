# nfs
If there is `no_root_squash` in the nfs share, follow this to copy a local bash binary as root and gain root on the victim machine

[https://book.hacktricks.xyz/linux-unix/privilege-escalation/nfs-no\_root\_squash-misconfiguration-pe](https://book.hacktricks.xyz/linux-unix/privilege-escalation/nfs-no_root_squash-misconfiguration-pe) 

If there is `root_squash`, the folders might be owned by `nobody:nogroup` and unaccessible(even with root!).

But if we created the same local user as on the remote system, we could access it. Specifically `william` with it's user id 1003: `useradd -u 3003 william && su william`. This get's us into the mounted folder