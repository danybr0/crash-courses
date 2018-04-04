# SQL Recap commands

SQL or Structured Query Language is a language designed to manage data in a Relational Database Management System (RDBMS).

This article is perfect if you need to brush up your knowledge on SQL for an interview.


## Database Related Commands

### See currently available databases

`SHOW DATABASES;`

### Create a new database

`CREATE DATABASE <database_name>;`

### Select a database to use

`USE <database_name>;`

### Import SQL commands from .sql file

`SOURCE <path_of_.sql_file>;`

### Delete a database

`DROP DATABASE <database_name>;`


## Table Related Commands

### See currently available tables in a database

`SHOW TABLES;`

### Create a new table

`CREATE TABLE <table_name1> (
    <col_name1> <col_type1>,
    <col_name2> <col_type2>,
    <col_name3> <col_type3>
    PRIMARY KEY (<col_name1>),
    FOREIGN KEY (<col_name2>) REFERENCES <table_name2>(<col_name2>)
);`

Integrity Constraints in CREATE TABLE

You may need to set constraints for certain columns of a table. Following constraints can be imposed while creating a table.

* NOT NULL
* PRIMARY KEY (col_name1, col_name2,…)
* FOREIGN KEY (col_namex1, …, col_namexn) REFERENCES table_name(col_namex1, …, col_namexn)

You can include more than one primary key which will create a composite or concatenated primary key.

Example
Create the table instructor.

`CREATE TABLE instructor (
    ID CHAR(5),
    name VARCHAR(20) NOT NULL,
    dept_name VARCHAR(20),
    salary NUMERIC(8,2),
    PRIMARY KEY (ID),
    FOREIGN KEY (dept_name) REFERENCES department(dept_name))`

### Describe columns of a table

You can view the columns of a table with details such as the type and key, using the command given below.

`DESCRIBE <table_name>;`

### Insert into a table

`INSERT INTO <table_name> (<col_name1>, <col_name2>, <col_name3>, …)
    VALUES (<value1>, <value2>, <value3>, …);`

If you are inserting values to all the columns of a table, then there is no need to specify the column names at the beginning.

`INSERT INTO <table_name>
    VALUES (<value1>, <value2>, <value3>, …);`

### Update a table

`UPDATE <table_name>
    SET <col_name1> = <value1>, <col_name2> = <value2>, ...
    WHERE <condition>;`

### Delete all contents of a table

`DELETE FROM <table_name>;`

### Delete a table

`DROP TABLE <table_name>;`


## Querying Related Commands

### SELECT

The **SELECT** statement is used to select data from a particular table.

`SELECT <col_name1>, <col_name2>, …
     FROM <table_name>;`

You can select all the contents of a table as follows.

`SELECT * FROM <table_name>;`

### SELECT DISTINCT

A column of a table can often contain duplicate values. **SELECT DISTINCT** allows you to retrieve the distinct values.

`SELECT DISTINCT <col_name1>, <col_name2>, …
     FROM <table_name>;`

### WHERE

You can use **WHERE** keyword in a **SELECT** statement in order to include conditions for your data.

`SELECT <col_name1>, <col_name2>, …
     FROM <table_name>
     WHERE <condition>;`

You can include conditions consisting of,

* Comparison of **text**
* Comparison of **numbers**
* Logical operations including **AND**, **OR** and **NOT**.

**Example**

Go through the following example statements. Note how conditions have been included with the **WHERE** clause.

`SELECT * FROM course WHERE dept_name=’Comp. Sci.’;
SELECT * FROM course WHERE credits>3;
SELECT * FROM course WHERE dept_name='Comp. Sci.' AND credits>3;`

### GROUP BY
