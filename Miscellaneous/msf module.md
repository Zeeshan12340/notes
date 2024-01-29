# msf module
to load a custom module in metasploit, copy the `.rb` script into `/usr/share/metasploit-framework/modules/exploits/`(where it's relevant) and use `reload_all` to load the script. 

Note: It might show up as auxiliary, just use the directoy path in msfconsole.

```text-plain
cewl -w list.txt -d 5 -m 5 http://thm.labs
```

\-w will write the contents to a file. In this case, list.txt.

\-m 5 gathers strings (words) that are 5 characters or more

\-d 5 is the depth level of web crawling/spidering (default 2)

http://thm.labs is the URL that will be used