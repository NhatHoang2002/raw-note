---
layout: post
title: "DataQuest - Data Engineer 1: Postgres for Data Engineers"
categories: [data, python]
tags: [dataquest, python, data]
toc: 1
comment: 1
date: 2019-05-23
---

This note is used for my notes about the [Data Engineer path](https://www.dataquest.io/path/data-engineer) on **dataquest**. I take this note after I have some basics [on python]({{site.url}}/tags#python) and followed 45% [Data Scientist path](https://www.dataquest.io/path/data-scientist) (also on Dataquest).

{% include toc.html %}

{% assign img-url = '/images/posts/data/dataquest' %}

## Mission 245 - Intro To Postgres ([PostgreSQL](https://www.postgresql.org/))

- [PostgreSQL documentation](https://www.postgresql.org/docs/).
- [**Faker**](http://faker.rtfd.org) is a Python package that generates fake data for you.

### Becoming a Data Engineer

{% include more.html content="[C'est quoi, le Big Data](/files/dataquest/big-data.pdf)." %}

- **Aim**: learn strategies to deal with petabytes of data, automating intensive queries, and understanding the architecture of a robust data platform.
- Essentially, a data engineer needs to have the skills to build a data pipeline that connects all the pieces of the data ecosystem together and keep it up and running.
	![Data pipeline]({{img-url}}/m245-1.svg){:.w-700}
- we have dedicated this section to focus on a type of data storage called a **relational database**.

### Connecting to Postgres

- **[SQLite](https://www.sqlite.org/)** as it is one of the most common database engines that is used.
- SQLite contains most of the SQL commands that are used with bigger engines which means *<mark>if you know SQLite, you know the basics of every other SQL database</mark>*.
- The biggest **drawbacks** of SQLite in a data production system are due to its positves in development. Because of its simple use case, 
	- SQLite was **not built for multiple connections**. 
	- SQLite only allows a single process to write to the database 
	- **making it difficult to share with multiple people and services**.
- Remember that the **goal of the data engineer** is to <mark>unlock the data platform to a wide group of analysts, data scientists, or any other interested member in an organization</mark>.
- We would be better off using another open source database engine called **Postgres**.
- Postgres is a much more robust engine that is **implemented as a server rather than a single file**.
	- This type of a design is called a **client-server** model where clients can interact with the server. 
- **protocol**, which is a set of rules that both the client and server have agreed to (*language that both the client and server will use when the client requests and the server responds with data.*)
-  In Python, there is an open source library called **[psycopg2](http://initd.org/psycopg/)** that implements the Postgres protocol to connect to our Postgres server. You can think of psycopg2 being similar to connecting to a SQLite database using the **[sqlite3](https://docs.python.org/3.5/library/sqlite3.html)** library.
- To connect to a database using psycopg2
	~~~ python
	import psycopg2
	conn = psycopg2.connect("dbname=postgres user=postgres")
	print(connect)
	connect.close()
	~~~ 

### Interacting with the Database

- [Connection classs/object](http://initd.org/psycopg/docs/connection.html).
	- The connection object creates a **client session** with the database server that instantiates a **persistent client** to speak with.
- To issue commands against the database, you will also need to create a **[Cursor object](http://initd.org/psycopg/docs/cursor.html)** using the Connection object.
	~~~ python
	import psycopg2
	conn = psycopg2.connect("dbname=postgres user=postgres")
	cur = conn.cursor()
	cur.execute('SELECT * FROM users')
	one = cur.fetchone() # returns the first result or None
	all = cur.fetchall() # returns a list of each row in the table or an empty list []
	~~~
- the cur object calls the execute method and, if it is successful, it **will return `None`**.
	~~~ python
	import psycopg2
	conn = psycopg2.connect("dbname=dq user=dq")
	cur = conn.cursor()
	cur.execute('SELECT * FROM notes') # query to select all
	notes = cur.fetchall() # fetch all the results
	conn.close() # close the connection
	~~~

### Creating a table

- Create a table
	~~~ python
	CREATE TABLE tableName(
	   column1 dataType1 PRIMARY KEY,
	   column2 dataType2,
	   column3 dataType3,
	   ...
	);
	~~~
- To delete the table from the database
	~~~ python
	DROP TABLE tableName

	DROP TABLE IF EXISTS tableName
	~~~
- If you have issues when running your code, you should execute the `DROP TABLE` command before creating the table
	~~~ python
	conn = psycopg2.connect("dbname=dq user=dq")
	cur = conn.cursor()
	cur.execute("DROP TABLE IF EXISTS example")
	cur.execute("CREATE TABLE example(count INTEGER)")
	~~~
- Example,
~~~ python
import psycopg2
conn = psycopg2.connect("dbname=dq user=dq")
cur = conn.cursor()
cur.execute(
    "CREATE TABLE users(id integer PRIMARY KEY, email text, name text, address text);"
    )
~~~

### SQL Transactions

- Transactions prevent this type of behavior by ensuring that all the queries in a transaction block are executed at the same time.
  - Two users request 2 different demands but they affect on the same data.
  - If any of the transactions fail, the whole group fails, and no changes are made to the database at all.
- PostgreSQL engine only run when the *commit* is called. All queries request are made before the commit is called. Therefore, postgresql only consider all the queriest at once!
- We can use `rollback` if we don't want to apply the changes ub the tracsaction.

~~~ python
import psycopg2
conn = psycopg2.connect("dbname=dq user=dq")
cur = conn.cursor()
cur.execute(
    "CREATE TABLE users(id integer PRIMARY KEY, email text, name text, address text);"
)
conn.commit() # commit to apply the changes in the transaction to the database
conn.close() # close the connection
~~~

### Inserting the data



