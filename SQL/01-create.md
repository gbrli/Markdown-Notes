# Create

Goorm IDE used to run MySQL for Udemy course: https://ide.goorm.io/my/dashboard

Goorm commands: `mysql-clt cli`, `source file.sql`

## Database Commands
```
SHOW databases; 
CREATE DATABASE soap_store; 
DROP DATABASE hello_world_db; 
USE soap_store;
SELECT database();
```
## Table Commands
```
SHOW TABLES;
SHOW COLUMNS FROM tablename;
DESC tablename;
DROP TABLE cats; 
```
## Table Creation Example
```
CREATE TABLE pastries
 (
    name VARCHAR(50) NOT NULL DEFAULT 'x',
    quantity INT NOT NULL DEFAULT 99
 );
 ```
## Inserting Data Into a Freshly Baked Table
Variables can be inserted in a different order as long as they match what the table has been create with, much like an OOP constructor.
```
INSERT INTO cats(name, age) VALUES ('Jetson', 7);
INSERT INTO cats(age, name) VALUES (3, 'Meow');
INSERT INTO cats(age, name) VALUES (3, 'Meow'), (5, 'Zak'), (7, 'Klang') ;
```
# Data Types
## Strings
**CHAR** is faster for strings but it has a fixed length. CHAR(5) means any character over 5 will be truncated. It is best used for data that is always the same length, like M/F or Y/N. Otherwise, use **VARCHAR(255)** for strings.
## Numbers
Both **INTEGER** and **DECIMALS** are exact-value types. DECIMAL (5,2) means the number is 5 digits long with 2 decimals (250.10). Inserting 123456 would be saved as 999.99. Rounding occurs on 1.999 to 2.00. 

**FLOAT** and DOUBLE** use less memory than DECIMAL, but they are approximate values. Only use DOUBLE as it stores more data, or just use DECIMAL.
## Dates
**DATE** stores a date as DD-MM-YYYY.

**TIME** stores the time as HH:MM:SS.

**DATETIME** stores both combined.

**CURDATE**, **CURTIME** and **NOW** do the same, inserting the current date and time when the data is inserted. 

**TIMESTAMPS** work the same way but they range from 1970 to 2038 and takes less space. It is used mostly for storing metadata.
```
CREATE TABLE people (name VARCHAR(100), birthdate DATE, birthtime TIME, birthdt DATETIME);
INSERT INTO people (name, birthdate, birthtime, birthdt) 
VALUES('NewNameWithCurrentDate', CURDATE(), CURTIME(), NOW());
```
## Formatting Dates
Format dates like the examples below:
```
SELECT DAYOFWEEK(NOW());
SELECT DAYNAME(NOW());

SELECT DATE_FORMAT(NOW(), '%m/%d/%Y ');
SELECT DATE_FORMAT(NOW(), '%m/%D');
SELECT DATE_FORMAT(birthdt, '%m/%d/%Y at %h:%i on a %W') FROM people;
```
Using **TIMESTAMP**:
```
CREATE TABLE tweets (
   content VARCHAR(240), 
   username VARCHAR(20), 
   created_at TIMESTAMP DEFAULT NOW());

INSERT INTO tweets (
   content, 
   username) 
VALUES (
   "me sa ch'ho fatto lo stronzo",
   'arfonso');
```


# Bits and Bobs
## Primary and Foreign Keys
**Primary key** constraints will uniquely identify a record in a table. They cannot be NULL and using AUTO_INCREMENT creates a new a id with each row.

**Foreign keys** are used when joining multiple tables - see Joins later.

```
cat_id INT AUTO_INCREMENT NOT NULL PRIMARY KEY
```
NULL means a value is not known.
NOT NULL means the value is an integer 0, or an empty string. Don't use ~~WHERE breed = NULL~~.
```
SELECT * FROM cats WHERE breed IS NULL;
```
This exists:
```
SHOW WARNINGS;
```
