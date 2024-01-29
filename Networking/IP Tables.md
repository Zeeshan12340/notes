# IP Tables
`sudo iptables -A INPUT -p tcp --dport ssh -j ACCEPT`

`sudo iptables -A INPUT -p tcp --dport smb -j DROP`

The implicit deny rule states "if I have not explicitly allowed something through the Firewall, then DENY it implicitly, without hesitation". It is essentially a catch-all for anything else that you don't want to specifically add a rule for. We can make this rule with 

`sudo iptables -A INPUT -j DROP`

Unfortunately, iptables is not saved in memory and needs to be configured each time you reboot your machine. This can be troublesome and annoying for any system admin. Restarting a server is probably an uncommon event but nonetheless, can happen. In order to save iptables configuration, you can enter `sudo iptables-save`

`sudo ufw <allow/deny> <port>/<optional: protocol>`

`sudo ufw allow 9000/tcp`