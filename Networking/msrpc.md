# msrpc
port 135, Microsoft Remote Procedure Call, also known as a function call or a subroutine call, is a protocol that uses the client-server model in order to allow one program to request service from a program on another computer without having to understand the details of that computer's network. MSRPC was originally derived from open source software but has been developed further and copyrighted by Microsoft.

Depending on the host configuration, the RPC endpoint mapper can be accessed through TCP and UDP port 135, via SMB with a null or authenticated session (TCP 139 and 445), and as a web service listening on TCP port 593.

**Identifying Exposed RPC Services:**

```text-plain
rpcdump [-p port] 192.168.189.1
```

[https://www.blackhillsinfosec.com/password-spraying-other-fun-with-rpcclient/](https://www.blackhillsinfosec.com/password-spraying-other-fun-with-rpcclient/) 

[https://www.samba.org/samba/docs/current/man-html/rpcclient.1.html](https://www.samba.org/samba/docs/current/man-html/rpcclient.1.html) 

To login annonymously, use:

```text-plain
rpcclient -U % 10.10.172.129 or rpcclient -U "" -N 10.10.172.129
```

Useful commands with rpcclient:

```text-plain
enumdomusers, enumdomgroups, querygroup <rid>, queryuser <rid>, getdompwinfo 
```