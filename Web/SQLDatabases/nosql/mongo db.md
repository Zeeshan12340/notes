# mongo db
MongoDB allows you to group multiple documents with a similar function together in higher hierarchy structures called **collections** for organizational purposes. Collections are the equivalent of tables in relational databases. Continuing with our HR example, all the employee's documents would be conveniently grouped in a collection called "people" as shown in the diagram below. 

![](mongo%20db/Z3mI9BS.png)

As with any database, a special language is used to retrieve information from the database. Just as relational databases use some variant of SQL, non-relational databases such as MongoDB use NoSQL. In general terms, NoSQL refers to any way of querying a database that is not SQL, meaning it may vary depending on the database used.

![](mongo%20db/vGT21GY.png)

If we wanted to build a filter so that only the documents where the last\_name is "Sandler" are retrieved, our filter would look like this:  
 

`**['last_name' => 'Sandler']**`

As a result, this query only retrieves the second document.

If we wanted to filter the documents where the gender is male, and the last\_name is Phillips, we would have the following filter:

`**['gender' => 'male', 'last_name' => 'Phillips']**`

This would only return the first document.

If we wanted to retrieve all documents where the age is less than 50, we could use the following filter:

`**['age' => ['$lt'=>'50']]**`

he web application is making a query to MongoDB, using the "**myapp**" database and "**login**" collection, requesting any document that passes the filter `**['username'=>$user, 'password'=>$pass]**`, where both **$user** and **$pass** are obtained directly from HTTP POST parameters

If somehow we could send an array to the **$user** and **$pass** variables with the following content:

`**$user = ['$ne'=>'xxxx']**` 

`**$pass = ['$ne'=>'yyyy']**` 

The resulting filter would end up looking like this:

`**['username'=>['$ne'=>'xxxx'], 'password'=>['$ne'=>'yyyy']]**`