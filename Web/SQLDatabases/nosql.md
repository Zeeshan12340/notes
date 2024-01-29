# nosql
it’s used to refer to non-relational databases that are growing in popularity as the back-end for distributed cloud platforms and web applications. Instead of storing data in tables, as with relational databases, NoSQL data stores use other data models that are better suited for specific purposes, such as documents, graphs, objects, and many others. 

The major exception is that the information isn't stored on tables but rather in **documents**.

With traditional [SQL injection](https://www.netsparker.com/website-security-scanner/sql-injection-vulnerability-scanner/), the attacker exploits unsafe user input processing to modify or replace SQL queries (or other SQL statements) that the application sends to a database engine. In other words, an SQL injection allows the attacker to execute commands in the database. Unlike relational databases, NoSQL databases don't use a common query language. NoSQL query syntax is product-specific and queries are written in the programming language of the application: PHP, JavaScript, Python, Java, and so on. This means that a successful injection lets the attacker execute commands not only in the database, but also in the application itself, which can be far more dangerous.

[https://www.invicti.com/blog/web-security/what-is-nosql-injection/](https://www.invicti.com/blog/web-security/what-is-nosql-injection/) 

[https://nullsweep.com/nosql-injection-cheatsheet/](https://nullsweep.com/nosql-injection-cheatsheet/) 

For nosql injection with a nodejs server, taking json requests we can use the following complete payload with the simple nosql payload of `{"$ne": 1}`

```text-plain
fetch('', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
        },
        body: JSON.stringify({username: {"$ne": 1}, password: {"$ne": 1}})
      }).then(() => {
        location.reload();})
```