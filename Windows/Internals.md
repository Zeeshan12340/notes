# Internals
`Sys-internals`
---------------

`\\live.sysinternals.com\tools\procmon.exe` in cmd , `Install-WindowsFeature WebDAV-Redirector –Restart`

Sysinternals Suite is divided into various categories, including:

*   Disk management
*   Process management
*   Networking tools
*   System information
*   Security tools

You can view alternate streams with `streams -accepteula file.txt` and open alternate stream with `notepad file.txt:stream.txt`

The [Microsoft docs](https://docs.microsoft.com/en-us/windows/win32/procthread/about-processes-and-threads) break down these other components, "Each process provides the resources needed to execute a program. A process has a virtual address space, executable code, open handles to system objects, a security context, a unique process identifier, environment variables, a priority class, minimum and maximum working set sizes, and at least one thread of execution."

Below are a few examples of default applications that start processes.

*   MsMpEng (Microsoft Defender)
*   wininit (keyboard and mouse)
*   lsass (credential storage)

|     |     |
| --- | --- |
| **Process Component** | **Purpose** |
| Private Virtual Address Space | Virtual memory addresses that the process is allocated. |
| Executable Program | Defines code and data stored in the virtual address space. |
| Open Handles | Defines handles to system resources accessible to the process. |
| Security Context | The access token defines the user, security groups, privileges, and other security information. |
| Process ID | Unique numerical identifier of the process. |
| Threads | Section of a process scheduled for execution. |

We can simplify the definition of a thread: "controlling the execution of a process."

Virtual memory provides each process with a [private virtual address space](https://docs.microsoft.com/en-us/windows/win32/memory/virtual-address-space). A memory manager is used to translate virtual addresses to physical addresses. By having a private virtual address space and not directly writing to physical memory, processes have less risk of causing damage.

The theoretical maximum virtual address space is 4 GB on a 32-bit x86 system.

This address space is split in half, the lower half (_0x00000000 - 0x7FFFFFFF_) is allocated to processes as mentioned above. The upper half (_0x80000000 - 0xFFFFFFFF_) is allocated to OS memory utilization. Administrators can alter this allocation layout for applications that require a larger address space through settings (_increaseUserVA_) or the [AWE (**A**ddress **W**indowing **E**xtensions)](https://docs.microsoft.com/en-us/windows/win32/memory/address-windowing-extensions).

DLLs are used as one of the core functionalities behind application execution in Windows. From the [Windows documentation](https://docs.microsoft.com/en-us/troubleshoot/windows-client/deployment/dynamic-link-library#:~:text=A%20DLL%20is%20a%20library,common%20dialog%20box%20related%20functions.), "The use of DLLs helps promote modularization of code, code reuse, efficient memory usage, and reduced disk space. So, the operating system and the programs load faster, run faster, and take less disk space on the computer."

DLLs can be loaded in a program using _load-time dynamic linking_ or _run-time dynamic linking_.

When loaded using _load-time dynamic linking_, explicit calls to the DLL functions are made from the application. You can only achieve this type of linking by providing a header (_.h_) and import library (_.lib_) file.

When loaded using _run-time dynamic linking_, a separate function (`LoadLibrary` or `LoadLibraryEx`) is used to load the DLL at run time. Once loaded, you need to use `GetProcAddress` to identify the exported DLL function to call.

|     |     |
| --- | --- |
| **Section** | **Purpose** |
| .text | Contains executable code and entry point |
| .data | Contains initialized data (strings, variables, etc.) |
| .rdata or .idata | Contains imports (Windows API) and DLLs. |
| .reloc | Contains relocation information |
| .rsrc | Contains application resources (images, etc.) |
| .debug | Contains debug information |