# Container environment 
Containers, due to their isolated nature, will often have very little processes running in comparison to something such as a virtual machine. We can simply use `ps aux` to print the running processes.

Containers allow environment variables to be provided from the host operating system by the use of a ".dockerenv" file. This file is located in the "/" directory, and would exist on a container - even if no environment variables were provided: `cd / && ls -lah`

Those pesky cgroups

Note how we utilised "cgroups" in Task 10. Cgroups are used by containerisation software such as LXC or Docker. Let's look for them with by navigating to "/proc/1" and then _catting_  the "cgroups" file...It is worth mentioning that the "cgroups" file contains paths including the word "docker"

[The Dirtyc0w kernel exploit](https://github.com/dirtycow/dirtycow.github.io)

[Exploiting runC (CVE-2019-5736)](https://unit42.paloaltonetworks.com/breaking-docker-via-runc-explaining-cve-2019-5736/)

[Trailofbits' capabilities demonstration](https://blog.trailofbits.com/2019/07/19/understanding-docker-container-escapes/#:~:text=The%20SYS_ADMIN%20capability%20allows%20a,security%20risks%20of%20doing%20so.)

[Cgroups101](https://docs.google.com/presentation/d/1WdByuxWgayPb-RstO-XaENSqVPGP7h6t3GS6W4jk4tk/htmlpresent)