---
title: "IBM Data Course 5: Databases and SQL for Data Science (Week 1 & Week 2)"
categories: [data]
tags: [data, ibm data, python, SQL]
toc: 1
comment: 1
date: 2019-04-05
---

{% assign img-url = '/images/posts/data/ibm' %}

This note was first taken when I learnt the [IBM Data Professional Certificate course](https://www.coursera.org/specializations/ibm-data-science-professional-certificate) on Coursera.

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
[Go back to Course 4](/ibm-data-professional-certificate-3).
</span>
</div>

{% include more.html content="[Go to Course 5 Week 3 & 4](/ibm-data-professional-certificate-5)." %}

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
- **CREATE** statement
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
	- Use the DEFAULT clause in the CREATE TABLE statement to specify the default value for the database server to insert into a column when no explicit value for the column is specified.
	- Use the CHECK clause to designate conditions that must be met before data can be assigned to a column during an INSERT or UPDATE statement.
- **SELECT** statement
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
		INSERT INTO <tablename> 
			(<col1>, <col2>,...) 
			VALUES 
				(<val1a>, <val2a>, ...), 
				(<val1b>, <val2b>, ...)
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
	- Different types of models
	- An **information model** is an abstract formal representation of entities that includes their properties, relationships, and the operations that can be performed on them.
	- **An information model** is at the conceptual level and defines relationships between objects. 
	- **Data models** are defined in a more concrete level, are specific and include details.
		- **The hierarchical model** organizes its data using a tree structure
		- **The relational model** is the most used data model for databases
			- Allows for data independence
			- Data is stored in tables with entity relationships
		- An **entity-relationship data** model or **ER data model**, is an alternative to a relational data model.
	- The building blocks of an **ER diagram** are **entities** and **attributes**. 
		- **Entities have attributes**, which are the data elements that characterize the entity. 
		- Attributes tell us more about the entity. 
		- Ex: book -> entity, attributes -> book title, year,...
		- Entity -> table in database
		- Atributes -> columns in the table
	- A table containing one or more foreign keys is called a **Dependent table**.
- **Types of relationship** between entities
	- Building blocks of relationship are
		- Entities sets: rectangle
		- Relationship sets: diamond with lines conneting associated entities.
		- Crows foot notations: > \| < symbols
		- Attributes: ovals
		![ER Diagram of Author]({{img-url}}/ibm-4-1.png){:.w-500}
	- **One-to-One** relationship: one book must be written by one author
	![One-to-One relationship]({{img-url}}/ibm-4-2.png){:.w-500}
	- **One-to-Many** relationship or **Many-to-One** relationship: A book written by many authors.
	![One-to-Many relationship]({{img-url}}/ibm-4-3.png){:.w-500}
	- **Many-to-Many** relationship: many authors write many books.
	![Many-to-Many relationship]({{img-url}}/ibm-4-4.png){:.w-500}
- **Mapping entities to tables**
	- **ERD** = Entity relational diagram
	![Entity book]({{img-url}}/ibm-4-5.png){:.w-500}
- **Relational model concepts**
	- Relational model: based on the concept of relation.
	- relational dabase
		- a set of relations
		- relation = mathematical term for table
		- 2 parts
			- **relational schema**
			- **relational instance**
		- Relational Schema: name of a relation and attributes
		- Relational Instance: a table made up of attributes or columns.
			- column = attributes = field
			- Row = tuple
		- Relation: degree & cardinality
			- **degree** = the number of columns/attributes in a relation
			- **cardinality** = the number of tuples/rows
	![Degree and Cardinality]({{img-url}}/ibm-4-6.png){:.w-500}


## Week 2: Advanced SQL

How to create databses + upload csv files to cooperate with them on IBM Clound Db2? Check the instruction on week 2 (***Week2Lab1v4-RA.pdf***)

### String Patterns, Ranges, Sorting, and Grouping

- **Using String Patterns, Ranges**
	- Retrieving rows from a table
	![Retrieving rows from a table]({{img-url}}/ibm-4-7.png){:.w-700}
	- **String Pattern**: in the case we don't know/remember exactly the key to apply to `WHERE`
		~~~ sql
		SELECT firstname 
			FROM author
			WHERE firstname like 'R%'
		~~~
	- **Range**
		~~~ sql
		SELECT title, pages
			FROM book
			WHERE pages >= 290 AND pages <= 300
		
		SELECT title, pages
			FROM book
			WHERE pages BETWEEN 290 AND 300
		~~~
	- **Set of Values**

		~~~ sql
		SELECT firstname, lastname, country
			FROM author
			WHERE country='AU' OR country='BR'
		
		SELECT firstname, lastname, country
			FROM author
			WHERE country IN ('AU', 'BR')
		~~~
- **Sorting result sets**
	- Use **ORDER BY** (`DESC` or `ASC` - default)
		~~~ sql
		SELECT title 
			FROM book
			ORDER BY title DESC
		
		SELECT title, pages
			FROM book
			ORDER BY 2 -- column 2 (pages)
		~~~
- **Grouping Result Sets**
	- **DISTINCT**: eliminating duplicates
		~~~ sql
		SELECT DISTINCT(country)
			FROM author
		~~~
	- **GROUP BY**: count the number of row has the same values
		~~~ sql
		SELECT country, COUNT(country) 
			FROM author 
			GROUP BY country
		
		SELECT country, COUNT(country)
			AS count -- create a column named "count" containing the numbers
			FROM author
			GROUP BY country
		~~~
	- **HAVING**: check more than 4 authors from the same country, only works with the GROUP BY clause.
		~~~ sql
		SELECT country, COUNT(country)
			AS count
			FROM author
			GROUP BY country
			HAVING COUNT(country) > 4
		~~~

### Functions, Sub-Queries, Multiple Tables

- **built-in functions** to perform operations on data right within the database.
- reduces network traffic and use of bandwidth
- It is also possible to **create your own functions** in the database
- One of the limitations of built-in aggregate functions like AVG() is that they cannot always be evaluated in the WHERE clause -> need to use sub-queries!!

![Petsale table]({{img-url}}/ibm-4-8.png){:.w-700}

- Add up all the values in the SALEPRICE column and explicitly name the output column SUM_OF_SALEPRICE
	~~~ sql
	SELECT SUM(SALEPRICE) AS SUM_OF_SALEPRICE FROM PETSALE
	~~~
- Maximum QUANTITY of any ANIMAL sold:
	~~~ sql
	select MAX(QUANTITY) from PETSALE
	~~~
- Average value of SALEPRICE :
	~~~ sql
	select AVG(SALEPRICE) from PETSALE
	~~~
- Average SALEPRICE per 'Dog' :
	~~~ sql
	select AVG( SALEPRICE / QUANTITY ) from PETSALE where ANIMAL = 'Dog'
	~~~
- Round UP/DOWN every value in SALEPRICE column to nearest integer:
	~~~ sql
	select ROUND(SALEPRICE) from PETSALE
	~~~
- Retrieve the length of each value in ANIMAL column
	~~~ sql
	select LENGTH(ANIMAL) from PETSALE
	~~~
- Retrieve the ANIMAL column values in UPPERCASE format
	~~~ sql
	select UCASE(ANIMAL) from PETSALE
	~~~
- Use the function in a WHERE clause
	~~~ sql
	select * from PETSALE where LCASE(ANIMAL) = 'cat'
	~~~
- Use DISTINCT() function to get unique values
	~~~ sql
	select DISTINCT(UCASE(ANIMAL)) from PETSALE
	~~~

**Date, Time functions**: Functions exist to extract the DAY, MONTH, DAYOFMONTH, DAYOFWEEK, DAYOFYEAR, WEEK, HOUR, MINUTE, SECOND.

- Extract the DAY portion from a date
~~~ sql
select DAY(SALEDATE) from PETSALE where ANIMAL = 'Cat'
~~~
- Get the number of sales during the month of may (i.e. month 5):
~~~ sql
select COUNT(*) from PETSALE where MONTH(SALEDATE)='05'
~~~
- You can also perform DATE or TIME arithmetic
~~~ sql
select (SALEDATE + 3 DAYS) from PETSALE
~~~
- Special registers CURRENT TIME and CURRENT DATE are also available:
~~~ sql
select (CURRENT DATE - SALEDATE) from PETSALE
~~~

### Sub-Queries and Nested Selects

- One of the limitations of built-in aggregate functions like AVG() is that they cannot always be evaluated in the WHERE clause.
- we want to retrieve the list of employees who earn more than the average salary.
	~~~ sql
	select EMP_ID, F_NAME, L_NAME, SALARY from employees 
		where SALARY < 
	 		(select AVG(SALARY) from employees);
	~~~
- The IN operator can also be used and there can be multiple leves of sub-queries, such as:
	~~~ sql
	select EMP_ID, F_NAME, L_NAME, DEP_ID from employees 
	 where DEP_ID IN  
	 ( select DEP_ID from employees where DEP_ID > 
	         ( select MIN(DEP_ID) from employees ) 
	 );
	~~~
- The sub-select doesn't just have to go in the where clause, it can also go in other parts of the query such as in the list of columns to be selected:
	~~~ sql
	select EMP_ID, SALARY,
		( select AVG(SALARY) from employees ) 
		AS AVG_SALARY
	  	from employees ;
	
	select * 
		from 
		( select EMP_ID, F_NAME, L_NAME, DEP_ID 
			from employees) ;
	~~~

### Working with multiple tables

There are several ways to access multiple tables in the same query:

1. Sub-queries
2. Implicit **JOIN**
3. **JOIN** operators (INNER JOIN, OUTER JOIN, etc.)

![Petsale table]({{img-url}}/ibm-4-9.png){:.w-700}

1. **Sub-queries**
	- retrieve only the employee records that correspond to departments in the DEPARTMENTS table
		~~~ sql
		select * from employees 
		  where DEP_ID IN
		  ( select DEPT_ID_DEP from departments );
		~~~
	- we want to retrieve only the list of employees from a specific location
		~~~ sql
		select * from employees 
		  where DEP_ID IN
		   ( select DEPT_ID_DEP from departments 
		     where LOC_ID = 'L0002' );
		~~~
	- retrieve the department ID and name for Empolyees who earn more than 70000:
	~~~ sql
	select DEPT_ID_DEP, DEP_NAME from departments
	 where DEPT_ID_DEP IN
	  ( select DEP_ID from employees 
	    where SALARY > 70000 ) ;
	~~~
2. **Implicit JOIN**
	- full join
		~~~ sql
		select * from employees, departments;
		~~~
	-  we limit the result set to only rows with matching department IDs:
		~~~ sql
		select * from employees, departments 
		  where employees.DEP_ID = departments.DEPT_ID_DEP;
		~~~
	- Since the table names can be sometimes long, we can use shorther aliases for table names as follows:
		~~~ sql
		select * from employees E, departments D 
		  where E.DEP_ID = D.DEPT_ID_DEP;
		~~~
	- the column names in the select clause can be pre-fixed by aliases:
		~~~ sql
		select E.EMP_ID, D.DEPT_ID_DEP  
		  from employees E, departments D 
		  where E.DEP_ID = D.DEPT_ID_DEP;
	~~~
	- we want to see the department name for each employee:
		~~~ sql
		select E.EMP_ID, D.DEP_NAME from 
		  employees E, departments D
		  where E.DEP_ID = D.DEPT_ID_DEP
		~~~
3. **JOIN OPERATOR**

Check at [Go to Course 5 Week 3 & 4](/ibm-data-professional-certificate-5)