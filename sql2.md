
## The SQL CREATE DATABASE Statement

The CREATE DATABASE statement is used to create a new SQL database.

### Syntax

CREATE  DATABASE  _databasename_;

----------

## CREATE DATABASE Example

The following SQL statement creates a database called "testDB":

### Example

CREATE  DATABASE  testDB;
## SQL FOREIGN KEY on CREATE TABLE

The following SQL creates a FOREIGN KEY on the "PersonID" column when the "Orders" table is created:

**MySQL:**

CREATE  TABLE  Orders (  
OrderID int  NOT  NULL,  
OrderNumber int  NOT  NULL,  
PersonID int,  
PRIMARY  KEY  (OrderID),  
FOREIGN  KEY  (PersonID)  REFERENCES  Persons(PersonID)  
);

**SQL Server / Oracle / MS Access:**

CREATE  TABLE  Orders (  
OrderID int  NOT  NULL  PRIMARY  KEY,  
OrderNumber int  NOT  NULL,  
PersonID int  FOREIGN  KEY  REFERENCES  Persons(PersonID)  
);

To allow naming of a FOREIGN KEY constraint, and for defining a FOREIGN KEY constraint on multiple columns, use the following SQL syntax:

**MySQL / SQL Server / Oracle / MS Access:**

CREATE  TABLE  Orders (  
OrderID int  NOT  NULL,  
OrderNumber int  NOT  NULL,  
PersonID int,  
PRIMARY  KEY  (OrderID),  
CONSTRAINT  FK_PersonOrder  FOREIGN  KEY  (PersonID)  
REFERENCES  Persons(PersonID)  
);

----------

## SQL FOREIGN KEY on ALTER TABLE

To create a FOREIGN KEY constraint on the "PersonID" column when the "Orders" table is already created, use the following SQL:

**MySQL / SQL Server / Oracle / MS Access:**

ALTER  TABLE  Orders  
ADD  FOREIGN  KEY  (PersonID)  REFERENCES  Persons(PersonID);

To allow naming of a FOREIGN KEY constraint, and for defining a FOREIGN KEY constraint on multiple columns, use the following SQL syntax:

**MySQL / SQL Server / Oracle / MS Access:**

ALTER  TABLE  Orders  
ADD  CONSTRAINT  FK_PersonOrder  
FOREIGN  KEY  (PersonID)  REFERENCES  Persons(PersonID);

----------

## DROP a FOREIGN KEY Constraint

To drop a FOREIGN KEY constraint, use the following SQL:

**MySQL:**

ALTER  TABLE  Orders  
DROP  FOREIGN  KEY  FK_PersonOrder;

**SQL Server / Oracle / MS Access:**

ALTER  TABLE  Orders  
DROP  CONSTRAINT  FK_PersonOrder;
**Note:**  Be careful before dropping a database. Deleting a database will result in loss of complete information stored in the database!

----------

## DROP DATABASE Example

The following SQL statement drops the existing database "testDB":

### Example

DROP  DATABASE  testDB;

**Tip:**  Make sure you have admin privilege before dropping any database. Once a database is dropped, you can check it in the list of databases with the following SQL command: SHOW DATABASES;

## The SQL BACKUP DATABASE Statement

The BACKUP DATABASE statement is used in SQL Server to create a full back up of an existing SQL database.

### Syntax

BACKUP  DATABASE  _databasename_  
TO  DISK  =  '_filepath_';

----------

## The SQL BACKUP WITH DIFFERENTIAL Statement

A differential back up only backs up the parts of the database that have changed since the last full database backup.

### Syntax

BACKUP  DATABASE  _databasename_  
TO  DISK  =  '_filepath_'  
WITH  DIFFERENTIAL;

----------

## BACKUP DATABASE Example

The following SQL statement creates a full back up of the existing database "testDB" to the D disk:

### Example

BACKUP  DATABASE  testDB  
TO  DISK  =  'D:\backups\testDB.bak';

**Tip:**  Always back up the database to a different drive than the actual database. If you get a disk crash, you will not lose your backup file along with the database.

----------

## BACKUP WITH DIFFERENTIAL Example

The following SQL statement creates a differential back up of the database "testDB":

### Example

BACKUP  DATABASE  testDB  
TO  DISK  =  'D:\backups\testDB.bak'  
WITH  DIFFERENTIAL;

## The SQL CREATE TABLE Statement

The CREATE TABLE statement is used to create a new table in a database.

### Syntax

CREATE  TABLE  _table_name_ (  
_column1 datatype_,  
_column2 datatype_,  
_column3 datatype_,  
....  
);

The column parameters specify the names of the columns of the table.

The datatype parameter specifies the type of data the column can hold (e.g. varchar, integer, date, etc.).

**Tip:**  For an overview of the available data types, go to our complete  [Data Types Reference](https://www.w3schools.com/sql/sql_datatypes.asp).

----------

## SQL CREATE TABLE Example

The following example creates a table called "Persons" that contains five columns: PersonID, LastName, FirstName, Address, and City:

### Example

CREATE  TABLE  Persons (  
PersonID int,  
LastName varchar(255),  
FirstName varchar(255),  
Address varchar(255),  
City varchar(255)  
);

## The SQL DROP TABLE Statement

The DROP TABLE statement is used to drop an existing table in a database.

### Syntax

DROP  TABLE  _table_name_;

**Note****:**  Be careful before dropping a table. Deleting a table will result in loss of complete information stored in the table!

----------

## SQL DROP TABLE Example

The following SQL statement drops the existing table "Shippers":

### Example

DROP  TABLE  Shippers;

[Try it Yourself »](https://www.w3schools.com/sql/trysql.asp?filename=trysql_drop_table)

----------

## SQL TRUNCATE TABLE

The TRUNCATE TABLE statement is used to delete the data inside a table, but not the table itself.

### Syntax

TRUNCATE  TABLE  _table_name_;

## SQL ALTER TABLE Statement

The ALTER TABLE statement is used to add, delete, or modify columns in an existing table.

The ALTER TABLE statement is also used to add and drop various constraints on an existing table.

----------

## ALTER TABLE - ADD Column

To add a column in a table, use the following syntax:

ALTER  TABLE  _table_name_  
ADD  _column_name datatype_;

The following SQL adds an "Email" column to the "Customers" table:

### Example

ALTER  TABLE  Customers  
ADD  Email varchar(255);

[Try it Yourself »](https://www.w3schools.com/sql/trysql.asp?filename=trysql_alter_table)

----------

## ALTER TABLE - DROP COLUMN

To delete a column in a table, use the following syntax (notice that some database systems don't allow deleting a column):

ALTER  TABLE  _table_name_  
DROP  COLUMN  _column_name_;

The following SQL deletes the "Email" column from the "Customers" table:

### Example

ALTER  TABLE  Customers  
DROP  COLUMN  Email;

SQL Create Constraints
Constraints can be specified when the table is created with the CREATE TABLE statement, or after the table is created with the ALTER TABLE statement.

Syntax
CREATE TABLE table_name (
    column1 datatype constraint,
    column2 datatype constraint,
    column3 datatype constraint,
    ....
);

## SQL Constraints

SQL constraints are used to specify rules for the data in a table.

Constraints are used to limit the type of data that can go into a table. This ensures the accuracy and reliability of the data in the table. If there is any violation between the constraint and the data action, the action is aborted.

Constraints can be column level or table level. Column level constraints apply to a column, and table level constraints apply to the whole table.

The following constraints are commonly used in SQL:

NOT NULL - Ensures that a column cannot have a NULL value
UNIQUE - Ensures that all values in a column are different
PRIMARY KEY - A combination of a NOT NULL and UNIQUE. Uniquely identifies each row in a table
FOREIGN KEY - Uniquely identifies a row/record in another table
CHECK - Ensures that all values in a column satisfies a specific condition
DEFAULT - Sets a default value for a column when no value is specified
INDEX - Used to create and retrieve data from the database very quickly
## SQL NOT NULL Constraint

By default, a column can hold NULL values.

The NOT NULL constraint enforces a column to NOT accept NULL values.

This enforces a field to always contain a value, which means that you cannot insert a new record, or update a record without adding a value to this field.

----------

## SQL NOT NULL on CREATE TABLE

The following SQL ensures that the "ID", "LastName", and "FirstName" columns will NOT accept NULL values when the "Persons" table is created:

### Example

CREATE  TABLE  Persons (  
ID int  NOT  NULL,  
LastName varchar(255)  NOT  NULL,  
FirstName varchar(255)  NOT  NULL,  
Age int  
);


## SQL NOT NULL on ALTER TABLE

To create a NOT NULL constraint on the "Age" column when the "Persons" table is already created, use the following SQL:

ALTER  TABLE  Persons  
MODIFY  Age int  NOT  NULL;

## SQL UNIQUE Constraint

The UNIQUE constraint ensures that all values in a column are different.

Both the UNIQUE and PRIMARY KEY constraints provide a guarantee for uniqueness for a column or set of columns.

A PRIMARY KEY constraint automatically has a UNIQUE constraint.

However, you can have many UNIQUE constraints per table, but only one PRIMARY KEY constraint per table.

----------

## SQL UNIQUE Constraint on CREATE TABLE

The following SQL creates a UNIQUE constraint on the "ID" column when the "Persons" table is created:

**SQL Server / Oracle / MS Access:**

CREATE  TABLE  Persons (  
ID int  NOT  NULL  UNIQUE,  
LastName varchar(255)  NOT  NULL,  
FirstName varchar(255),  
Age int  
);

**MySQL:**

CREATE  TABLE  Persons (  
ID int  NOT  NULL,  
LastName varchar(255)  NOT  NULL,  
FirstName varchar(255),  
Age int,  
UNIQUE  (ID)  
);

To name a UNIQUE constraint, and to define a UNIQUE constraint on multiple columns, use the following SQL syntax:

**MySQL / SQL Server / Oracle / MS Access:**

CREATE  TABLE  Persons (  
ID int  NOT  NULL,  
LastName varchar(255)  NOT  NULL,  
FirstName varchar(255),  
Age int,  
CONSTRAINT  UC_Person  UNIQUE  (ID,LastName)  
);
## SQL PRIMARY KEY Constraint

The PRIMARY KEY constraint uniquely identifies each record in a table.

Primary keys must contain UNIQUE values, and cannot contain NULL values.

A table can have only one primary key, which may consist of single or multiple fields.

----------

## SQL PRIMARY KEY on CREATE TABLE

The following SQL creates a PRIMARY KEY on the "ID" column when the "Persons" table is created:

**MySQL:**

CREATE  TABLE  Persons (  
ID int  NOT  NULL,  
LastName varchar(255)  NOT  NULL,  
FirstName varchar(255),  
Age int,  
PRIMARY  KEY  (ID)  
);
## SQL DEFAULT Constraint

The DEFAULT constraint is used to provide a default value for a column.

The default value will be added to all new records IF no other value is specified.

----------

## SQL DEFAULT on CREATE TABLE

The following SQL sets a DEFAULT value for the "City" column when the "Persons" table is created:

**My SQL / SQL Server / Oracle / MS Access:**

CREATE  TABLE  Persons (  
ID int  NOT  NULL,  
LastName varchar(255)  NOT  NULL,  
FirstName varchar(255),  
Age int,  
City varchar(255)  DEFAULT  'Sandnes'  
);

The DEFAULT constraint can also be used to insert system values, by using functions like GETDATE():

CREATE  TABLE  Orders (  
ID int  NOT  NULL,  
OrderNumber int  NOT  NULL,  
OrderDate date  DEFAULT  GETDATE()  
);
## SQL CREATE INDEX Statement

The CREATE INDEX statement is used to create indexes in tables.

Indexes are used to retrieve data from the database very fast. The users cannot see the indexes, they are just used to speed up searches/queries.

**Note:**  Updating a table with indexes takes more time than updating a table without (because the indexes also need an update). So, only create indexes on columns that will be frequently searched against.

### CREATE INDEX Syntax

Creates an index on a table. Duplicate values are allowed:

CREATE  INDEX  _index_name_  
ON  _table_name_  (_column1_,  _column2_, ...);

### CREATE UNIQUE INDEX Syntax

Creates a unique index on a table. Duplicate values are not allowed:

CREATE  UNIQUE  INDEX  _index_name_  
ON  _table_name_  (_column1_,  _column2_, ...);

**Note:**  The syntax for creating indexes varies among different databases. Therefore: Check the syntax for creating indexes in your database.

## AUTO INCREMENT Field

Auto-increment allows a unique number to be generated automatically when a new record is inserted into a table.

Often this is the primary key field that we would like to be created automatically every time a new record is inserted.

----------

## Syntax for MySQL

The following SQL statement defines the "Personid" column to be an auto-increment primary key field in the "Persons" table:

CREATE  TABLE  Persons (  
Personid int  NOT  NULL  AUTO_INCREMENT,  
LastName varchar(255)  NOT  NULL,  
FirstName varchar(255),  
Age int,  
PRIMARY  KEY  (Personid)  
);

MySQL uses the AUTO_INCREMENT keyword to perform an auto-increment feature.

By default, the starting value for AUTO_INCREMENT is 1, and it will increment by 1 for each new record.

To let the AUTO_INCREMENT sequence start with another value, use the following SQL statement:

ALTER  TABLE  Persons AUTO_INCREMENT=100;

To insert a new record into the "Persons" table, we will NOT have to specify a value for the "Personid" column (a unique value will be added automatically):

INSERT  INTO  Persons (FirstName,LastName)  
VALUES  ('Lars','Monsen');

The SQL statement above would insert a new record into the "Persons" table. The "Personid" column would be assigned a unique value. The "FirstName" column would be set to "Lars" and the "LastName" column would be set to "Monsen".