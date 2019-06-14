---
layout: post
title: "Codecademy - Data Science 1"
categories: [data]
tags: [data, data codecademy, codecademy]
comment: 1
toc: 1
date: 2019-06-10
---

{% assign img-url = '/images/posts/codecademy/data' %}

This note is created when I started to learn the [Data Science](https://www.codecademy.com/paths/data-science) on Codecademy.

## A day in life - Data Analyst

- Data extraction with SQL
- Programming basics with Python
- Data analysis using pandas, a Python library
- Data visualization using Matplotlib, a Python library
- Machine Learning using scikit-learn, a Python library

## Relational Database Management System (RDMS)

- RDBMS use **SQL** language to access the database.
- Popular RDBMS: 
  - **SQLite**: 
    - all of the data can be stored locally
    - popular choice for databases in cellphones, PDAs, MP3 players, set-top boxes, and other electronic gadgets. <mark>The SQL courses on Codecademy use SQLite.</mark>
  - **MySQL**:
    - the most popular open source SQL database
    - easy to use, inexpensive, reliable, large community of developers
    - poor performance when scaling, open source development has lagged 
    - does not include some advanced features that developers may be used to
  - **PostgreSQL**:
    - open source SQL database
    - shares many of the same advantages of MySQL
    - foreign key support without requiring complex configuration.
    - slower in performance than other databases
  - **Oracle DB**:
    - not open sourced (Oracle Corporation owns)
    - for large applications, particularly in the banking industry
  - **SQL Server**:
    - Microsoft owns
    - Large enterprise applications mostly use SQL Server.
    - offers a free entry-level version called Express

## SQL

- J**[ust look up at this site](https://www.w3schools.com/sql/sql_delete.asp)**!
- `ALTER TABLE` statement adds a new column to a table. 

  ~~~ sql
  ALTER TABLE celebs 
  ADD COLUMN twitter_handle TEXT;
  ~~~

- **Constraints** that add information about how a column can be used are invoked after specifying the data type for a column.

  ~~~ sql
  CREATE TABLE celebs (
     id INTEGER PRIMARY KEY, 
     name TEXT UNIQUE,
     date_of_birth TEXT NOT NULL,
     date_of_death TEXT DEFAULT 'Not Applicable'
  );
  ~~~

- `AS`

  ~~~ sql
  SELECT name AS 'ten'
  FROM movies;
  ~~~

- `DISTINCT` is used to return unique values in the output. It filters out all duplicate values in the specified column(s).
- `LIKE` can be a useful operator when you want to compare similar values. Check [this](https://www.w3schools.com/sql/sql_like.asp) for other usesages.
- A `CASE` statement allows us to create different outputs (usually in the SELECT statement). It is SQL’s way of handling if-then logic.
- [Cross join](https://www.w3resource.com/sql/joins/cross-join.php)
- `with` statements

  ~~~ sql
  WITH previous_results AS (
     SELECT ...
     ...
     ...
     ...
  )
  SELECT *
  FROM previous_results
  JOIN customers
    ON _____ = _____;
  ~~~


## Numpy with Statistics

- `np.percentile(d, 40)` gives the number which divides array `d` into 40% and 60%.
- 

