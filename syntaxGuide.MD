# **MySQL Cheat Sheet**


### How to login into mysql from terminal

You first have to log into your terminal with ssh (ex. ssh as@167.114.138.180 -p 6597). This will bring you into the computers shell. From there you can log into MySQL with the command: sudo mysql -u root -p followed by your password.

### How to SHOW USERS

Use this command once logged into MySQL: <br>
select * from mysql.user;

### How to CREATE USERS
Use this command:<br>
CREATE USER 'new_user'@'localhost' IDENTIFIED BY 'password';


### How to GRANT PRIVILEGES, Show granted privileges and remove.

Use this command to grant all privileges: <br>
GRANT ALL PRIVILEGES ON database_name.* TO 'username'@'localhost';

Use this command to show granted privileges:
SHOW GRANTS;

Use this command to remove granted privileges:
REVOKE privileges ON database_name FROM user;

### How to SHOW, DELETE & CREATE DATABASES & SELECT DATABASES

Show Database: SHOW DATABASES; <br>
Create Database: CREATE DATABASE database_name;<br>
Delete Database: DELETE DATABASE datbase_name;<br>
Select Database: USE DATABASE database_name;

### How to CREATE a TABLE with Columns and their data types

Here is an example:<br>
CREATE TABLE table_name (<br>
    ID INT NOT NULL PRIMARY KEY AUTO_INCREMENT, <br>
    Name VARCHAR(255),<br>
    Surname VARCHAR(255),<br>
    PhoneNum INT,<br>
    Date DATE<br>
);<br>
In this example the columns are: ID, Name, Surname, PhoneNum and Date The data types are VARCHAR(255) which allows for up to 255 characters, INT which allows for integers and DATE which allows for the date to be entered (year/month/day) 

### How to SHOW, DELETE & DROP Tables

First you need to be in the database that the table you want to drop or delete is in. Then, to delete or drop a table you type: <br>
DROP TABLE table_name;

### How to Insert ROWS & RECORDS (single and multiple)

Here is an example:

INSERT INTO table_name
    (ID,Date,Time,CalledNum,Seconds) VALUES
        (101,'1979-03-20','2014-02-20 09.00.00',8888888,650),
        (102,'1985-01-11','2012-01-10 08.00.00',7777777,750),
        (103,'1999-11-21','2009-02-11 07.00.00',9999999,450),
        (104,'1992-08-03','2011-03-02 06.00.00',5555555,950);
In the example the column names that are having info inserted into are listed in between the brakets in order and the info to be inserted follows the word VALUES. Dates and VARCHAR need quotes, INT doesn't.        
### How to SELECT with the WHERE Clause

Here is an example:<br>
SELECT * FROM table_name
WHERE column_name=column_entry;
In this example the print out will be the entry in the row where it matches the column_name and column_entry.

### How to SELECT with the WHERE Clause using a range

The BETWEEN operator selects values within a given range. The values can be numbers, text, or dates.

The BETWEEN operator is inclusive: begin and end values are included.<br>
Example:<br>
SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2;

### How to DELETE an individual ROW

Here is n example:
DELETE FROM table_name WHERE column_name=rowToBeDeleted;
In the example the information within that row will be deleted.

### How to UPDATE a ROW

Here is an example:
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
In this example, use the where statement to taget a specific row to update.
### How to add a new column and modify it

Here is an example:
ALTER TABLE table_name
MODIFY COLUMN column_name datatype;
After choosing the column_name and entering a new column_name after MODIFY COLUMN enter the data type such as VARCHAR or INT.

### How to Order by and use Distinct

The ORDER BY keyword sorts the records in ascending order by default. To sort the records in descending order, use the DESC keyword.
Example:
SELECT column1, column2, ...
FROM table_name
ORDER BY column1, column2, ... ASC|DESC;<br>

The SELECT DISTINCT statement is used to return only distinct (different) values.

Inside a table, a column often contains many duplicate values; and sometimes you only want to list the different (distinct) values.<br>
Example:
SELECT DISTINCT Column_name FROM table_name;


### How to Concatenate Columns
Here is an example of how to concantenate 3 columns into 1 address column:<br>
SELECT CONCAT(Address, " ", PostalCode, " ", City) AS Address
FROM Customers;
This will take the original address column, the postalcode column and the city column and put them together as a new address column.

### How to Select Distinct Rows

The SELECT DISTINCT statement is used to return only distinct (different) values.

Inside a table, a column often contains many duplicate values; and sometimes you only want to list the different (distinct) values.<br>
Example:<br>
SELECT DISTINCT column1, column2, ...
FROM table_name;

### How to use LIKE to Search

The LIKE operator is used in a WHERE clause to search for a specified pattern in a column.

There are two wildcards often used in conjunction with the LIKE operator:

 The percent sign (%) represents zero, one, or multiple characters
 The underscore sign (_) represents one, single character<br>
 You can also combine any number of conditions using AND or OR operators<br>
 Here are the Wildcards that can be used with the LIKE operator:<br>
 LIKE Operator	Description
WHERE CustomerName LIKE 'a%'	Finds any values that start with "a"
WHERE CustomerName LIKE '%a'	Finds any values that end with "a"
WHERE CustomerName LIKE '%or%'	Finds any values that have "or" in any position
WHERE CustomerName LIKE '_r%'	Finds any values that have "r" in the second position
WHERE CustomerName LIKE 'a_%'	Finds any values that start with "a" and are at least 2 characters in length
WHERE CustomerName LIKE 'a__%'	Finds any values that start with "a" and are at least 3 characters in length
WHERE ContactName LIKE 'a%o'	Finds any values that start with "a" and ends with "o" 
 Example:<br>
 SELECT * FROM Customers
WHERE CustomerName LIKE '_r%';

### How Select using IN

The IN operator allows you to specify multiple values in a WHERE clause.

The IN operator is a shorthand for multiple OR conditions.<br>
Example:<br>
SELECT column_name(s)
FROM table_name
WHERE column_name IN (value1, value2, ...);
or:

SELECT column_name(s)
FROM table_name
WHERE column_name IN (SELECT STATEMENT);

### How to Create & Remove Index

The CREATE INDEX statement is used to create indexes in tables.

Indexes are used to retrieve data from the database more quickly than otherwise. The users cannot see the indexes, they are just used to speed up searches/queries.<br>
Example:<br>
CREATE INDEX index_name
ON table_name (column1, column2, ...);<br>
You can also use UNIQUE when creating in index but you can not duplicate values.<br>
Example: <br>
CREATE UNIQUE INDEX index_name
ON table_name (column1, column2, ...);<br>
The DROP INDEX statement is used to delete an index in a table.<br>
Example:<br>
ALTER TABLE table_name
DROP INDEX index_name;

### Create Two Tables demonstrating a one to many relationship that shows a PK & FK

The FOREIGN KEY constraint is used to prevent actions that would destroy links between tables.

A FOREIGN KEY is a field (or collection of fields) in one table, that refers to the PRIMARY KEY in another table.

The table with the foreign key is called the child table, and the table with the primary key is called the referenced or parent table.<br>
Example:<br>
CREATE TABLE Orders (
    OrderID int NOT NULL,
    OrderNumber int NOT NULL,
    PersonID int,
    PRIMARY KEY (OrderID),
    FOREIGN KEY (PersonID) REFERENCES Persons(PersonID)
);
### How to use Inner Join
The INNER JOIN keyword selects records that have matching values in both tables.<br>
Example:<br>
SELECT column_name(s)
FROM table1
INNER JOIN table2
ON table1.column_name = table2.column_name;


### How to JOIN Multiple Tables

A JOIN clause is used to combine rows from two or more tables, based on a related column between them.<br>
Example:<br>
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate
FROM Orders
INNER JOIN Customers ON Orders.CustomerID=Customers.CustomerID;
