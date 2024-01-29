# WSH
```text-vbscript
Dim message 
message = "Welcome to THM"
MsgBox message
##########################
Set shell = WScript.CreateObject("Wscript.Shell")
shell.Run("C:\Windows\System32\calc.exe " & WScript.ScriptFullName),0,True
```

Another trick. If the VBS files are blacklisted, then we can rename the file to .txt file and run it using wscript as follows,

`wscript /e:VBScript  <file>`