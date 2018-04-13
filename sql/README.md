# SQL Recap commands

SQL or Structured Query Language is a language designed to manage data in a Relational Database Management System (RDBMS).

This article is perfect if you need to brush up your knowledge on SQL for an interview.

**NOTE**: Some database systems require a semicolon to be inserted at the end of each statement. The semicolon is the standard way to indicate the end of each SQL statement. I will be using **MySQL** for the examples, which requires a semicolon at the end of each statement.


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

_Integrity Constraints in CREATE TABLE_**

You may need to set constraints for certain columns of a table. Following constraints can be imposed while creating a table.

* __NOT NULL__
* __PRIMARY KEY__ (col_name1, col_name2,…)
* __FOREIGN KEY__ (col_namex1, …, col_namexn) REFERENCES table_name(col_namex1, …, col_namexn)

You can include more than one primary key which will create a **composite** or **concatenated primary key**.

**Example**
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

The **GROUP BY** statement is often used with **aggregate functions** such as **COUNT**, **MAX**, **MIN**, **SUM** and **AVG** to group the result-set.

**Example**
List the number of courses for each department.

`SELECT COUNT(course_id), dept_name
     FROM course
     GROUP BY dept_name;`

### HAVING

The **HAVING** clause was introduced to SQL because the **WHERE** keyword could not be used to compare values of **aggregate functions**.

`SELECT <col_name1>, <col_name2>, ...
    FROM <table_name>
    GROUP BY <column_namex>
    HAVING <condition>`

**Example**

List the number of courses for each department which offers more than one course.

`SELECT COUNT(course_id), dept_name
    FROM course
    GROUP BY dept_name
    HAVING COUNT(course_id)>1;`

### ORDER BY

**ORDER BY** is used to **sort a result set in ascending or descending order**. ORDER BY will sort in ascending order if you do not specify ASC or DESC.

`SELECT <col_name1>, <col_name2>, …
FROM <table_name>
ORDER BY <col_name1>, <col_name2>, … ASC|DESC;`

**Example**

List the courses in ascending and descending order of number of credits.

`SELECT * FROM course ORDER BY credits;
SELECT * FROM course ORDER BY credits DESC;`

### BETWEEN

**BETWEEN** clause is used to **select data within a given range**. The values can be numbers, text or even dates.

`SELECT <col_name1>, <col_name2>, …
    FROM <table_name>
    WHERE <col_namex> BETWEEN <value1> AND <value2>;`

**Example**
List the instructors who get a salary in between 50 000 and 100 000.

`SELECT * FROM instructor
    WHERE salary BETWEEN 50000 AND 100000;`

### LIKE

The **LIKE** operator is used in a **WHERE** clause to search for a **specified pattern in text**.

There are two wildcard operators used with LIKE.

* % (Zero, one, or multiple characters)
* _ (A single character)

`SELECT <col_name1>, <col_name2>, …
    FROM <table_name>
    WHERE <col_namex> LIKE <pattern>;`

**Example**
List the courses where the course name contains “to” and the courses where the course_id starts with “CS-”.

`SELECT * FROM course WHERE title LIKE ‘%to%’;
SELECT * FROM course WHERE course_id LIKE 'CS-___';`

### IN

Using **IN** clause, you can allow **multiple values within a WHERE clause**.

`SELECT <col_name1>, <col_name2>, …
    FROM <table_name>
    WHERE <col_namen> IN (<value1>, <value2>, …);`

**Example**
List the students in the departments of Comp. Sci., Physics, and Elec. Eng.

`SELECT * FROM student
    WHERE dept_name IN (‘Comp. Sci.’, ‘Physics’, ‘Elec. Eng.’);`

### JOIN

**JOIN** is used to combine values of two or more tables based on common attributes within them. Figure 13 given below depicts the different types of SQL joins. Note the difference between **LEFT OUTER JOIN** and **RIGHT OUTER JOIN**.

`SELECT <col_name1>, <col_name2>, …
    FROM <table_name1>
    JOIN <table_name2>
    ON <table_name1.col_namex> = <table2.col_namex>;`

**Example 1**
Select all the courses with relevant department details.

`SELECT * FROM course
    JOIN department
    ON course.dept_name=department.dept_name;`

**Example 2**
Select all the prerequisite courses with their course details.

`SELECT prereq.course_id, title, dept_name, credits, prereq_id
    FROM prereq
    LEFT OUTER JOIN course
    ON prereq.course_id=course.course_id;`

**Example 3**
Select all the courses with their course details, regardless of whether or not they have prerequisites.

`SELECT course.course_id, title, dept_name, credits, prereq_id
    FROM prereq
    RIGHT OUTER JOIN course
    ON prereq.course_id=course.course_id;`

### Views

Views are virtual SQL tables created using a result set of a statement. It contains rows and columns and is very similar to a general SQL table. A view always shows up-to-date data within the database.

**CREATE VIEW**

`CREATE VIEW <view_name> AS
    SELECT <col_name1>, <col_name2>, …
    FROM <table_name>
    WHERE <condition>;`

**DROP VIEW**

`DROP VIEW <view_name>;`

**Example**
Create a view consisting of courses with 3 credits.

`CREATE VIEW my_view AS SELECT * FROM course WHERE credits=3;`

`SELECT * FROM my_view;`

### Aggregate Functions

These functions are used to obtain a cumulative result relevant to the data being considered. Following are the commonly used aggregate functions.

* __COUNT(col_name)__ — Returns the number of rows
* __SUM(col_name)__ — Returns the sum of the values in a given column
* __AVG (col_name)__ — Returns the average of the values of a given column
* __MIN(col_name)__ — Returns the smallest value of a given column
* __MAX(col_name)__ — Returns the largest value of a given column

### Nested Subqueries

Nested subqueries are SQL queries which include a **SELECT-FROM-WHERE** expression that is nested within another query.

**Example**
Find courses offered in Fall 2009 and in Spring 2010.

`SELECT DISTINCT course_id
    FROM section
    WHERE semester = ‘Fall’ AND year= 2009 AND course_id IN (
        SELECT course_id
            FROM section
            WHERE semester = ‘Spring’ AND year= 2010
    );`



** See The article on medium [article on medium]

[article on medium]: https://towardsdatascience.com/sql-cheat-sheet-for-interviews-6e5981fa797b
