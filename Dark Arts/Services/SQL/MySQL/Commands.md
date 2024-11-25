-- -
#### General Commands
```mysql
# Note: the caps are optional, can do either.
SHOW GRANTS; # show allowed queries for your logged in user

# interact w/ databases
CREATE DATABASE <db name>; # create a new database
SHOW DATABASES; # show available databases
USE <db name>; # Load a database by name

# interact w/ tables
SHOW TABLES; # show the tables on the loaded database
DESCRIBE logins; # list table structure/fields/columns
```
#### Creating a new table
```mysql
# General
CREATE TABLE logins ( # create a new table w/ fields
	id INT,
	username VARCHAR(100),
	pass VARCHAR(100),
	date_of_joining DATETIME
);

# set id field is a required field that cannot be null and is auto increment when a new ID value is set upon new entry to the table.
id INT NOT NULL AUTO_INCREMENT,

# ensure each username is unique, and is a required field for new entries
username VARCHAR(100) UNIQUE NOT NULL,

# Set default value on new entries if vvalue not provided
date_of_joining DATETIME DEFAULT NOW(),

# Set primary key, which will uniquely identify each record in the table, referring to all data of a record within a table for relational databses. 
PRIMARY KEY(<field name>)

# all configs above used:
CREATE TABLE logins (
	id INT NOT NULL AUTO_INCREMENT,
	username VARCHAR(100) UNIQUE NOT NULL,
	password VARCHAR(100) NOT NULL,
	date_of_joining DATETIME DEFAULT NOW(),
	PRIMARY KEY (id)
);
```
#### Adding values to table
```mysql
# note that in this example, we insert user-pass combos in cleartext. This is bad security practice, as passwords should ALWAYS be hashed/encrypted before storage. 
# insert new entry into table
INSERT INTO <tabl name> VALUES (col1_val, col2_val, col3_val, ...);
INSERT INTO logins VALUES(1, 'admin', 'p@ssw0rd', '2020-07-02');

# can omit unrequired columns:
INSERT INTO logins(username, password) VALUES('administrator', 'adm1n_p@ss');
```
#### Retrieve records
```mysql
# grab all records from a table:
SELECT * FROM <tabl name>;
SELECT * FROM logins;

# select specific columns
SELECT <col1>, <col2> FROM <tabl name>;
SELECT username, password FROM logins;
```
#### Remove Tables/DBs
```mysql
# Will delete the table or db specified permanently w/o warning 
DROP TABLE <tabl name>;
```
#### Alter 
Can be used to rename a table or change/delete/add a  new column to an existing table
```mysql
# Add new column to existing table
ALTER TABLE <tabl> ADD <col> <datatype>;
ALTER TABLE logins ADD newColumn INT;

# Rename existing column in existing table
ALTER TABLE <tabl> RENAME COLUMN <new col> TO <old col>;

# change existing column's data type
ALTER TABLE <tabl> MODIFY <col> <datatype>;

# delete a column
ALTER TABLE <tabl> DROP <col>;
```
#### Sorting
```mysql
# Sort by column, default will sort in ascending order 
SELECT * FROM <tabl> ORDER BY <col>;

# sort by column, descending order
SELECT * FROM <tabl> ORDER BY <col> DESC;

# sort by 2 columns, one ascending order other descending so it knows what to do if there is duplicate data in one column.
SELECT * FROM <tabl> ORDER BY <col1> DESC, <col2> ASC; 
```