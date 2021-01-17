# Databases and SQL

## Database

A database is a collection of information that is organized so that it can be
easily accessed, managed and updated. 

## Relational Database

A relational database is a type of database. It uses a structure that allows us
to identify and access data in relation to another piece of data in the
database. Often, data in a relational database is organized into tables. 

## Tables : Rows and Columns

Tables can have hundreds, thousands, sometimes even millions of rows of data.
These rows are often called records.

Tables can also have many columns of data. Columns are labeled with a
descriptive name (say, age for example) and have a specific data type. 

## Relational Database Management System

A relational database management system (RDBMS) is a program that allows you to
create, update, and administer a relational database. Most relational database
management systems use the SQL language to access the database. 

## SQL - Structured Query Language

SQL (Structured Query Language) is a programming language used to communicate
with data stored in a relational database management system. SQL syntax is
similar to the English language, which makes it relatively easy to write, read,
and interpret. 

Many RDBMSs use SQL (and variations of SQL) to access the data in tables. For
example, SQLite is a relational database management system. SQLite contains a
minimal set of SQL commands (which are the same across all RDBMSs). Other
RDBMSs may use other variants.

## Why do we need SQL?

    - Allows users to access data in the relational database management
      systems.
    - Allows users to describe the data.
    - Allows users to define the data in a database and manipulate that data.
    - Allows to embed within other languages using SQL modules, libraries &
      pre-compilers.
    - Allows users to create and drop databases and tables.
    - Allows users to create view, stored procedure, functions in a database.
    - Allows users to set permissions on tables, procedures and views.

## SQL Architecture

Following is a simple diagram showing the SQL Architecture 

SQL Query -> Query Language Processor -> DBMS Engine -> Physical Database
                        ^                     ^
                 Parser + Optimizer        File Manager + Transaction Manager

## Primary Key

    - A primary key is a field in a table which uniquely identifies each
      row/record in a database table. Primary keys must contain unique values.
      A primary key column cannot have NULL values.
    - A table can have only one primary key, which may consist of single or
      multiple fields. When multiple fields are used as a primary key, they are
      called a composite key.
    - If a table has a primary key defined on any field(s), then you cannot
      have two records having the same value of that field(s).

## Create Primary Key

Generally, the primary key is created while creating the database and the
table. The primary key can also be created after the creation of the table as
shown below. 

```sql
CREATE TABLE CUSTOMERS(
   ID       INT              NOT NULL,  // To set a primary key on this column ID
   NAME     VARCHAR (20)     NOT NULL,
   AGE      INT              NOT NULL,
   ADDRESS  CHAR (25) ,
   SALARY   DECIMAL (18, 2),       
   PRIMARY KEY (ID)
);

ALTER TABLE CUSTOMER ADD PRIMARY KEY (ID);
```

### Foreign Key

    - A foreign key is a key used to link two tables together. This is
      sometimes also called as a referencing key.
    - A Foreign Key is a column or a combination of columns whose values match
      a Primary Key in a different table.
    - The relationship between 2 tables matches the Primary Key in one of the
      tables with a Foreign Key in the second table.

## Example

Consider the following two tables, "Customers" and "Orders"

```sql
CREATE TABLE CUSTOMERS(
   ID   INT              NOT NULL,
   NAME VARCHAR (20)     NOT NULL,
   AGE  INT              NOT NULL,
   ADDRESS  CHAR (25) ,
   SALARY   DECIMAL (18, 2),       
   PRIMARY KEY (ID)
);

CREATE TABLE ORDERS (
   ID          INT        NOT NULL,
   DATE        DATETIME, 
   CUSTOMER_ID INT references CUSTOMERS(ID),
   AMOUNT     double,
   PRIMARY KEY (ID)
);
```

Once the tables have been created, the foreign key can be created using the
following syntax :

```sql
ALTER TABLE ORDERS 
   ADD FOREIGN KEY (Customer_ID) REFERENCES CUSTOMERS (ID);
```

## SQL Statements

DDL - Data Definition Language - CREATE, ALTER, DROP

DML - Data Manipulation Language - SELECT, INSERT, UPDATE, DELETE

DCL - Data Control Language - GRANT, REVOKE

TCL - Transaction Control Language - SAVEPOINT, ROLLBACK, COMMIT

## SELECT Query

The SQL SELECT statement is used to fetch the data from a database table which
returns this data in the form of a result table. These result tables are called
result-sets. 

```sql
SELECT column1, column2, columnN FROM table_name;
```

If you want to fetch all the fields available in the field, then you can use
the following syntax. 

```sql
SELECT * FROM table_name;
```

## Example

Consider the following "Customers" table.

+----+----------+-----+-----------+----------+
| ID | NAME     | AGE | ADDRESS   | SALARY   |
+----+----------+-----+-----------+----------+
|  1 | Ramesh   |  32 | Ahmedabad |  2000.00 |
|  2 | Khilan   |  25 | Delhi     |  1500.00 |
|  3 | kaushik  |  23 | Kota      |  2000.00 |
|  4 | Chaitali |  25 | Mumbai    |  6500.00 |
|  5 | Hardik   |  27 | Bhopal    |  8500.00 |
|  6 | Komal    |  22 | MP        |  4500.00 |
|  7 | Muffy    |  24 | Indore    | 10000.00 |
+----+----------+-----+-----------+----------+

```sql
SELECT ID, NAME, SALARY FROM CUSTOMERS; // Selecting columns 
```

## SQL Where

The SQL WHERE clause is used to specify a condition while fetching the data
from a single table or by joining with multiple tables. If the given condition
is satisfied, then only it returns a specific value from the table. You should
use the WHERE clause to filter the records and fetching only the necessary
records.

The WHERE clause is not only used in the SELECT statement, but it is also used
in the UPDATE, DELETE statement.

### Syntax : 

```sql
SELECT column1, column2, columnN 
FROM table_name
WHERE [condition]
```

## Example

Using the same "Customers" table as before and one would like to retrieve all
the names of customers who's age is greater than 20, the following query can be
used. 

```sql
SELECT CUSTOMERS.AGE from CUSTOMERS where AGE > 20;
// Can use DB name as prefix before column name.
```

## INSERT Query

The SQL INSERT INTO Statement is used to add new rows of data to a table in the
database. 

### Syntax :

There are two basic syntax's of the INSERT INTO statement which are shown below. 

```sql
INSERT INTO TABLE_NAME (column1, column2, column3,...columnN)  
VALUES (value1, value2, value3,...valueN);
```

### Example

```sql
INSERT INTO CUSTOMERS (ID,NAME,AGE,ADDRESS,SALARY)
VALUES (1, 'Ramesh', 32, 'Ahmedabad', 2000.00 );

INSERT INTO CUSTOMERS (ID,NAME,AGE,ADDRESS,SALARY)
VALUES (2, 'Khilan', 25, 'Delhi', 1500.00 );

INSERT INTO CUSTOMERS (ID,NAME,AGE,ADDRESS,SALARY)
VALUES (3, 'kaushik', 23, 'Kota', 2000.00 );

INSERT INTO CUSTOMERS (ID,NAME,AGE,ADDRESS,SALARY)
VALUES (4, 'Chaitali', 25, 'Mumbai', 6500.00 );

INSERT INTO CUSTOMERS (ID,NAME,AGE,ADDRESS,SALARY)
VALUES (5, 'Hardik', 27, 'Bhopal', 8500.00 );

INSERT INTO CUSTOMERS (ID,NAME,AGE,ADDRESS,SALARY)
VALUES (6, 'Komal', 22, 'MP', 4500.00 );
```

## SQL Joins

The SQL Joins clause is used to combine records from two or more tables in a
database. A JOIN is a means for combining fields from two tables by using
values common to each. 

Example

Consider the following tables : Customers and Orders

CUSTOMERS Table
+----+----------+-----+-----------+----------+
| ID | NAME     | AGE | ADDRESS   | SALARY   |
+----+----------+-----+-----------+----------+
|  1 | Ramesh   |  32 | Ahmedabad |  2000.00 |
|  2 | Khilan   |  25 | Delhi     |  1500.00 |
|  3 | kaushik  |  23 | Kota      |  2000.00 |
|  4 | Chaitali |  25 | Mumbai    |  6500.00 |
|  5 | Hardik   |  27 | Bhopal    |  8500.00 |
|  6 | Komal    |  22 | MP        |  4500.00 |
|  7 | Muffy    |  24 | Indore    | 10000.00 |
+----+----------+-----+-----------+----------+

ORDERS Table
+-----+---------------------+-------------+--------+
|OID  | DATE                | CUSTOMER_ID | AMOUNT |
+-----+---------------------+-------------+--------+
| 102 | 2009-10-08 00:00:00 |           3 |   3000 |
| 100 | 2009-10-08 00:00:00 |           3 |   1500 |
| 101 | 2009-11-20 00:00:00 |           2 |   1560 |
| 103 | 2008-05-20 00:00:00 |           4 |   2060 |
+-----+---------------------+-------------+--------+

Let us join these two tables with a SELECT Query : 

```sql
SELECT ID, NAME, AGE, AMOUNT
   FROM CUSTOMERS INNER JOIN ORDERS
   ON CUSTOMERS.ID = ORDERS.CUSTOMER_ID;
```

Different Types Of Joins

    - INNER JOIN
    - LEFT JOIN
    - RIGHT JOIN
    - FULL JOIN
