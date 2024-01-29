# Network Services
**FTP**
-------

ALWAYS check for parent directories with `cd ..` or `cd ~`

make sure to enable binary mode when downloading the  
two files.  
ftp> binary  
200 Type set to I.  
ftp> mget \*  
mget chatserver.exe? y

we can use python to interact with ftp if we don't have the ftp client installed on the machine:

```text-plain
from ftplib import FTP
ftp = FTP('ftp.mofo.pwn') #server name or ip
ftp.login('someuser', '04653cr37Passw0rdK06') #username, password
ftp.retrlines('LIST') #to list files
```

to download files

```text-plain
filename = 'creds.txt' # filename
localfile = open(filename, 'wb') #opening file on local/host machine
ftp.retrbinary('RETR ' + filename, localfile.write, 1024) #writing file
ftp.quit() #exit
```

tftp can used for windows machines for file transfer.

**SMB**
-------

SMB - Server Message Block Protocol - is a client-server communication protocol used for sharing access to files, printers, serial ports and other resources on a network. \[[source](https://searchnetworking.techtarget.com/definition/Server-Message-Block-Protocol)\]  
 

Servers make file systems and other resources (printers, named pipes, APIs) available to clients on the network. Client computers may have their own hard disks, but they also want access to the shared file systems and printers on the servers.

`smbclient //10.10.10.2/secret -u suit -p 445`

Very useful for viewing files:

`smbmount "\\\\10.10.240.253\\profiles"  /tmp/smb/mounted`

Recursively, download all directories in smb

```text-plain
smbclient '\\server\share'
mask ""
recurse ON
prompt OFF
cd 'path\to\remote\dir'
lcd '~/path/to/download/to/'
mget *
```

**Telnet**
----------

Telnet is an application protocol which allows you, with the use of a telnet client, to connect to and execute commands on a remote machine that's hosting a telnet server.   
 

The telnet client will establish a connection with the server. The client will then become a virtual terminal- allowing you to interact with the remote host.  
 

**Tcpdump**
-----------

use `sudo tcpdump -i tun0 ip proto  //icmp` to listen for icmp packets sent to your ip from remote locations

`sudo tcpdump port 110 -A`.

Useful to see if you're able to send packets to remote locations even though you're not getting a response back

**NFS**
-------

Download the bash executable to your Downloads directory. Then use "cp ~/Downloads/bash ." to copy the bash executable to the NFS share. The copied bash shell must be owned by a root user, you can set this using "sudo chown root bash"

Now, we're going to add the SUID bit permission to the bash executable we just copied to the share using "sudo chmod +\[permission\] bash". What letter do we use to set the SUID bit set using chmod?(+s)