---
title: "IBM Data Course 5: Databases and SQL for Data Science"
categories: [data]
tags: [data, ibm data, python, SQL]
toc: 1
comment: 1
---

{% assign img-url = '/images/posts/data/ibm' %}

This note was first taken when I learnt the [IBM Data Professional Certificate course](https://www.coursera.org/specializations/ibm-data-science-professional-certificate) on Coursera.

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
[Go back to Course 4](/ibm-data-professional-certificate-3).
</span>
</div>

{% include more.html content="[Go to Course 6](/ibm-data-professional-certificate-5)." %}

{% include toc.html %}

## Week 1: Introduction to Databases and Basic SQL

### Basics

- SQL is 1 of the top 3 skills for data scientist.
- SQL is used for communicating with databases (query data)
- SQL = Structured English Query Language
- **Data** is a collection of facts in the form of words, numbers or even pictures. 
- **Database** 
	- is a respository of data. 
	- It's a program that stores data.
	- provides the functionality for adding, modifying and querying that data
	- different kind of databases store data in diff forms.
	- Data stored in a tabular form is a **relational database**.
	- A set of software tools for the data in the database is called a **database management system** or **DBMS** for short. 
	- **RDBMS** = relational database management system
		- Example: MySQL, Oracle Database
- Basic commands: `CREATE`, `INSERT`, `SELECT`, `UPDATE`, `DELETE`.

### How to create a Database instance on Cloud?

- Advantages of using **Cloud Database**
	- ease of use
	- scalability
	- disaster recovery
- **An instance of the Cloud database** operates as a service that handles all application requests to work with the data and any of the databases managed by that instance.
- **IBM Db2 Warehouse on Cloud**
- [IBM Db2 service](https://console.bluemix.net/catalog/services/db2)
- [Page of apps](https://console.bluemix.net/dashboard/apps) (need to log in)

### Basic SQL

- DDL = Data Definition Language (define, change or drop data)
- DML = Data Manipulation Language (read and modify data)
- **The primary key** of a relational table uniquely identifies each row in a table.
- `CREATE` statement
	- Syntax
		~~~ sql
		create table TABLENAME (
		    COLUMN1 datatype,
		    COLUMN2 datatype,
		    COLUMN3, datatype,
		        ...
		    ) ;
		~~~
	- Example
		~~~ sql
		create table TEST (
		    ID integer,
		    NAME varchar(30)
		    );
		~~~
	- `ID int NOT NULL,` : it cannot contain a NULL or an empty value. 
	- `PRIMARY KEY (ID)` : If you look at the last row in the create table statement above you will note that we are using ID as a Primary Key and the database does not allow Primary Keys to have NULL values. 
	- A **Primary Key** is a unique identifier in a table, and using Primary Keys can help speed up your queries significantly.
		- It must contain a unique value for each row of data.
		- It cannot contain null values.
	- DROP table before creating it to ignore the duplication error
		~~~ sql
		drop table COUNTRY;
		create table COUNTRY (
		    ID integer PRIMARY KEY NOT NULL,
		    CCODE char(2),
		    NAME varchar(60)
		    );
		~~~
- `SELECT` statement
	- is **DML** which is used to read and modify data.
	- The output of a select statement is called the **Result Set** or a **Result Table**.
	- The order of columns displayed always matches the order in the SELECT statement.
	- used with **WHERE** with operators: `=, >, <, >=, <=, <>`
	- Examples
		~~~ sql
		select * from book
		
		select <col1>, <col2> from book
		
		select book_id, title from book WHERE book_id='B1'
		~~~
- **COUNT**
	-  To get the **total number of rows** in a given table, simply issue: `select COUNT(*) from tablename`
	-  retrieve the number of rows where the medal recipient is from CANADA: `select COUNT(COUNTRY) from MEDALS where COUNTRY='CANADA'`
- **DISTINCT** is used to remove duplicate values from a result set. 
	- To retrieve unique values in a column issue: `select DISTINCT columnname from tablename`
	- retrieve the list of unique countries that received GOLD medals, that is, removing all duplicate values of the same country: `select DISTINCT COUNTRY from MEDALS where MEDALTYPE = 'GOLD'`
- **LIMIT** is used for restricting the number of rows retrieved from the database. 
	- To retrieve just the first 10 rows in a table: `select * from tablename LIMIT 10`
	- This can be very useful to examine the result set by looking at just a few rows instead of retrieving the entire result set which may be very large. 
	- retrieve just a few rows in the MEDALS table for a 
	- particular year, you can issue: `select * from MEDALS where YEAR = 2018 LIMIT 5`
- **INSERT**
	- add new rows to the table
	- DML
	- You can insert 1 row, 2 rows, or more than two rows with a single INSERT statement.
	- Examples,
		~~~ sql
		INSERT INTO <tablename> (<col1>, <col2>,...) VALUES (<val1a>, <val2a>, ...), (<val1b>, <val2b>, ...)
		~~~
- **UPDATE** & **DELETE**
	- DML
	- Update
		~~~ sql
		UPDATE table_name
		SET column1 = value1, column2 = value2, ...
		WHERE condition;
		~~~
		- Be careful and specify a where clause if you intend to update just specific rows, otherwise **all rows will be updated**.
	- DELETE
		~~~ sql
		DELETE FROM table_name WHERE condition;
		~~~
		- If no `WHERE` clause is used, **all rows will be removed**.


### Relational database concepts

- **Information model** & **Data model**
	- 






