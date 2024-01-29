# Forensics
view “Applications and Services logs → Microsoft → windows → sysmon → operational” for sysmon logs

registry events have event ID 13/14, you can search for "pipe" events, but “Registry Run Keys/Start folder” shows any powershell scripts that interacted with registry keys

`Get-WinEvent -FilterHashtable @{logname="Microsoft-Windows-PrintService/Admin"} | fl`    

`**Get-WinEvent -Path .\Sysmon.evtx -FilterXPath ‘*/System/EventID=3’ | Sort-Object TimeCreated | fl**`