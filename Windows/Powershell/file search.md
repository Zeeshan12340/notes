# file search
Use Get-Childitem to search the files system with PowerShell. 

[https://devblogs.microsoft.com/scripting/use-windows-powershell-to-search-for-files/](https://devblogs.microsoft.com/scripting/use-windows-powershell-to-search-for-files/) 

`Get-Childitem –Path C:\ -Include *HSG* -Exclude *.JPG,*.MP3,*.TMP -File -Recurse -ErrorAction SilentlyContinue`