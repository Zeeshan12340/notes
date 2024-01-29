# Second Order SQLI
[https://portswigger.net/kb/issues/00100210\_sql-injection-second-order](https://portswigger.net/kb/issues/00100210_sql-injection-second-order) 

[https://infosecwriteups.com/the-wrath-of-second-order-sql-injection-c9338a51c6d](https://infosecwriteups.com/the-wrath-of-second-order-sql-injection-c9338a51c6d) 

Understanding Second-Order Code Injection
-----------------------------------------

Imagine a scenario wherein a malicious code injected into an application by an attacker which does not get immediately get executed in the application.   
Yes, you read that right. It’s a familiar story and it usually goes like this, user-provided data becomes a threat when it is utilized by the application or any other application wherein the injected code provided by the attacker gets activated resulting in successful exploitation.

The attacker injects into persistent storage (such as a table row) which is deemed as a trusted source. An attack is subsequently executed by another activity.

```text-plain
we can change the username, let’s change it to some sqli payload like ' or 1=1 -- a and then change the password.
If everything went right, the passwords of every user in the database now should be the same, but we dont have the username of another user to try to log in, or do we?
```

Description: SQL injection (second order)
-----------------------------------------

SQL injection vulnerabilities arise when user-controllable data is incorporated into database SQL queries in an unsafe manner. An attacker can supply crafted input to break out of the data context in which their input appears and interfere with the structure of the surrounding query.

A wide range of damaging attacks can often be delivered via SQL injection, including reading or modifying critical application data, interfering with application logic, escalating privileges within the database and taking control of the database server.

Second-order SQL injection arises when user-supplied data is stored by the application and later incorporated into SQL queries in an unsafe way. To detect the vulnerability, it is normally necessary to submit suitable data in one location, and then use some other application function that processes the data in an unsafe way.