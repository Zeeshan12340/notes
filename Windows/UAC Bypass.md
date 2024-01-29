# UAC Bypass
Even when we get a PowerShell session with an administrative user, UAC prevents us from performing any administrative tasks as we are currently using a filtered token only. If we want to take full control of our target, we must bypass UAC.

Running `msconfig` in `run` and going to `tools → Command Prompt` can allow for prompt-less privilege escalation if the current user is in the administrators group.

unlike `msconfig`, `azman.msc` has no intended built-in way to spawn a shell. To run a shell, we will abuse the application's help:

![](UAC%20Bypass/2f1aef0aa39ffcf9056999c939e43b.png) ![](UAC%20Bypass/43e3967d4cdb4c30dc46e7ce81eb28.png)

On the help screen, we will right-click any part of the help article and select **View Source.**

This will spawn a notepad process that we can leverage to get a shell. To do so, go to **File->Open** and make sure to select **All Files** in the combo box on the lower right corner. Go to `C:\Windows\System32` and search for `cmd.exe` and right-click to select Open: 

![](UAC%20Bypass/8ae24b569d5d95119e79feb425e1b7.png)

[https://docs.microsoft.com/en-us/windows/win32/com/the-com-elevation-moniker](https://docs.microsoft.com/en-us/windows/win32/com/the-com-elevation-moniker)