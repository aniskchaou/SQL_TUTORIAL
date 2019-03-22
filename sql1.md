## SQL Statements
-   SQL keywords are NOT case sensitive: **select is the same as SELECT**
Some database systems require a semicolon at the end of each SQL statement.

Semicolon is the standard way to separate each SQL statement in database systems that allow more than one SQL statement to be executed in the same call to the server.

In this tutorial, we will use semicolon at the end of each SQL statement.

----------

## Some of The Most Important SQL Commands

-   **SELECT**  - extracts data from a database
-   **UPDATE**  - updates data in a database
-   **DELETE**  - deletes data from a database
-   **INSERT INTO**  - inserts new data into a database
-   **CREATE DATABASE**  - creates a new database
-   **ALTER DATABASE**  - modifies a database
-   **CREATE TABLE**  - creates a new table
-   **ALTER TABLE**  - modifies a table
-   **DROP TABLE**  - deletes a table
-   **CREATE INDEX**  - creates an index (search key)
-   **DROP INDEX**  - deletes an index

## The SQL SELECT Statement

The SELECT statement is used to select data from a database.
The data returned is stored in a result table, called the result-set.

### SELECT Syntax

**SELECT**  _column1_, _column2, ..._  
**FROM**  _table_name_;

If you want to **select all the fields** available in the table, use the following syntax:

**SELECT** * **FROM** table_name;

## The SQL SELECT DISTINCT Statement

The SELECT DISTINCT statement is used to return only distinct (different) values.

Inside a table, a column often contains many duplicate values; and sometimes you only want to list the different (distinct) values.

### SELECT DISTINCT Syntax

SELECT  DISTINCT  _column1_, _column2, ..._  
FROM  _table_name_;

## SELECT DISTINCT Examples

The following SQL statement selects only the DISTINCT values from the "Country" column in the "Customers" table:

### Example

SELECT  DISTINCT  Country  FROM  Customers;

## The SQL WHERE Clause

**The WHERE clause is used to filter records.**
The WHERE clause is used to extract only those records that fulfill a specified condition.

### WHERE Syntax

**SELECT**  _column1_, _column2, ..._  
**FROM**  _table_name_  
**WHERE**  _condition_;

**Note:** The WHERE clause is not only used in SELECT statement, it is also used in UPDATE, DELETE statement, etc.!

## WHERE Clause Example

The following SQL statement selects all the customers from the country "Mexico", in the "Customers" table:

### Example

SELECT  *  FROM  Customers  
WHERE  Country='Mexico';

## Text Fields vs. Numeric Fields

SQL requires single quotes around text values (most database systems will also allow double quotes).

However, numeric fields should not be enclosed in quotes:

### Example

SELECT  *  FROM  Customers  
WHERE  CustomerID=1;

## Operators in The WHERE Clause

The following operators can be used in the WHERE clause:

Operator

Description

=

Equal

<>

Not equal.  **Note:**  In some versions of SQL this operator may be written as !=

>

Greater than

<

Less than

>=

Greater than or equal

<=

Less than or equal

BETWEEN

Between a certain range

LIKE

Search for a pattern

IN

To specify multiple possible values for a column
## The SQL AND, OR and NOT Operators

The WHERE clause can be combined with AND, OR, and NOT operators.

The AND and OR operators are used to filter records based on more than one condition:

-   The AND operator displays a record if all the conditions separated by AND are TRUE.
-   The OR operator displays a record if any of the conditions separated by OR is TRUE.

The NOT operator displays a record if the condition(s) is NOT TRUE.

### AND Syntax

**SELECT**  _column1_, _column2, ..._  
**FROM**  _table_name_  
*WHERE*  _condition1_  **AND**  _condition2_  **AND**  _condition3 ..._;

### OR Syntax

**SELECT**  _column1_, _column2, ..._  
**FROM**  _table_name_  
**WHERE**  _condition1_  **OR**  _condition2_  **OR**  _condition3 ..._;

### NOT Syntax

**SELECT**  _column1_, _column2, ..._  
**FROM**  _table_name_  
**WHERE**  **NOT**  _condition_;

## AND Example

The following SQL statement selects all fields from "Customers" where country is "Germany" AND city is "Berlin":

### Example

SELECT  *  FROM  Customers  
WHERE  Country='Germany'  AND  City='Berlin';


## OR Example

The following SQL statement selects all fields from "Customers" where city is "Berlin" OR "München":

### Example

SELECT  *  FROM  Customers  
WHERE  City='Berlin'  OR  City='München';


The following SQL statement selects all fields from "Customers" where country is "Germany" OR "Spain":

### Example

SELECT  *  FROM  Customers  
WHERE  Country='Germany'  OR  Country='Spain';


## NOT Example

The following SQL statement selects all fields from "Customers" where country is NOT "Germany":

### Example

SELECT  *  FROM  Customers  
WHERE  NOT  Country='Germany';



## Combining AND, OR and NOT

You can also combine the AND, OR and NOT operators.

The following SQL statement selects all fields from "Customers" where country is "Germany" AND city must be "Berlin" OR "München" (use parenthesis to form complex expressions):

### Example

SELECT  *  FROM  Customers  
WHERE  Country='Germany'  AND  (City='Berlin'  OR  City='München');


The following SQL statement selects all fields from "Customers" where country is NOT "Germany" and NOT "USA":

### Example

SELECT  *  FROM  Customers  
WHERE  NOT  Country='Germany'  AND  NOT  Country='USA';

## The SQL GROUP BY Statement

The GROUP BY statement is often used with aggregate functions (COUNT, MAX, MIN, SUM, AVG) to group the result-set by one or more columns.

### GROUP BY Syntax

SELECT  _column_name(s)_  
FROM  _table_name_  
WHERE  _condition_  
GROUP  BY  _column_name(s)  
_ORDER  BY  _column_name(s);_

## SQL GROUP BY Examples

The following SQL statement lists the number of customers in each country:

### Example

SELECT  COUNT(CustomerID), Country  
FROM  Customers  
GROUP  BY  Country;

## SQL HAVING Examples

The following SQL statement lists the number of customers in each country. Only include countries with more than 5 customers:

### Example

SELECT  COUNT(CustomerID), Country  
FROM  Customers  
GROUP  BY  Country  
HAVING  COUNT(CustomerID) >  5;

## The SQL EXISTS Operator

The EXISTS operator is used to test for the existence of any record in a subquery.

The EXISTS operator returns true if the subquery returns one or more records.

### EXISTS Syntax

SELECT  _column_name(s)_  
FROM  _table_name_  
WHERE  EXISTS  
(SELECT  _column_name_ FROM  _table_name_  WHERE  _condition_);
## SQL EXISTS Examples

The following SQL statement returns TRUE and lists the suppliers with a product price less than 20:

### Example

SELECT  SupplierName  
FROM  Suppliers  
WHERE  EXISTS  (SELECT  ProductName  FROM  Products  WHERE  SupplierId = Suppliers.supplierId  AND  Price <  20);


The following SQL statement returns TRUE and lists the suppliers with a product price equal to 22:

### Example

SELECT  SupplierName  
FROM  Suppliers  
WHERE  EXISTS  (SELECT  ProductName  FROM  Products  WHERE  SupplierId = Suppliers.supplierId  AND  Price =  22);

## The SQL ANY and ALL Operators

The ANY and ALL operators are used with a WHERE or HAVING clause.

The ANY operator returns true if any of the subquery values meet the condition.

The ALL operator returns true if all of the subquery values meet the condition.

### ANY Syntax

SELECT  _column_name(s)_  
FROM  _table_name_  
WHERE  _column_name operator_  ANY  
(SELECT  _column_name_ FROM  _table_name_  WHERE  _condition_);

### ALL Syntax

SELECT  _column_name(s)_  
FROM  _table_name_  
WHERE  _column_name operator_  ALL  
(SELECT  _column_name_ FROM  _table_name_ WHERE  _condition_);

## SQL ANY Examples

The ANY operator returns TRUE if any of the subquery values meet the condition.

The following SQL statement returns TRUE and lists the productnames if it finds ANY records in the OrderDetails table that quantity = 10:

### Example

SELECT  ProductName  
FROM  Products  
WHERE  ProductID =  ANY  (SELECT  ProductID  FROM  OrderDetails  WHERE  Quantity =  10);



The following SQL statement returns TRUE and lists the productnames if it finds ANY records in the OrderDetails table that quantity > 99:

### Example

SELECT  ProductName  
FROM  Products  
WHERE  ProductID =  ANY  (SELECT  ProductID  FROM  OrderDetails  WHERE  Quantity >  99);


## SQL ALL Example

The ALL operator returns TRUE if all of the subquery values meet the condition.

The following SQL statement returns TRUE and lists the productnames if ALL the records in the OrderDetails table has quantity = 10:

### Example

SELECT  ProductName  
FROM  Products  
WHERE  ProductID =  ALL  (SELECT  ProductID  FROM  OrderDetails  WHERE  Quantity =  10);

## The SQL SELECT INTO Statement

The SELECT INTO statement copies data from one table into a new table.

### SELECT INTO Syntax

Copy all columns into a new table:

SELECT  *  
INTO  _newtable_  [IN  _externaldb_]  
FROM  _oldtable  
_WHERE  _condition_;

Copy only some columns into a new table:

SELECT  _column1_,  _column2_,  _column3_, ...  
INTO  _newtable_  [IN  _externaldb_]  
FROM  _oldtable  
_WHERE  _condition;_

The new table will be created with the column-names and types as defined in the old table. You can create new column names using the AS clause.

----------

## SQL SELECT INTO Examples

The following SQL statement creates a backup copy of Customers:

SELECT  *  INTO  CustomersBackup2017  
FROM  Customers;

The following SQL statement uses the IN clause to copy the table into a new table in another database:

SELECT  *  INTO  CustomersBackup2017  IN  'Backup.mdb'  
FROM  Customers;

The following SQL statement copies only a few columns into a new table:

SELECT  CustomerName, ContactName  INTO  CustomersBackup2017  
FROM  Customers;

The following SQL statement copies only the German customers into a new table:

SELECT  *  INTO  CustomersGermany  
FROM  Customers  
WHERE  Country =  'Germany';

The following SQL statement copies data from more than one table into a new table:

SELECT  Customers.CustomerName, Orders.OrderID  
INTO  CustomersOrderBackup2017  
FROM  Customers  
LEFT  JOIN  Orders  ON  Customers.CustomerID = Orders.CustomerID;

**Tip:**  SELECT INTO can also be used to create a new, empty table using the schema of another. Just add a WHERE clause that causes the query to return no data:

SELECT  *  INTO  _newtable_  
FROM  _oldtable_  
WHERE  1  =  0;

## The SQL INSERT INTO SELECT Statement

The INSERT INTO SELECT statement copies data from one table and inserts it into another table.

-   INSERT INTO SELECT requires that data types in source and target tables match
-   The existing records in the target table are unaffected

### INSERT INTO SELECT Syntax

Copy all columns from one table to another table:

INSERT  INTO  _table2_  
SELECT  *  FROM  _table1  
_WHERE  _condition_;

Copy only some columns from one table into another table:

INSERT  INTO  _table2_ (_column1_,  _column2_,  _column3_, ...)  
SELECT  _column1_,  _column2_,  _column3_, ...  
FROM  _table1_  
WHERE  _condition_;
## SQL INSERT INTO SELECT Examples

The following SQL statement copies "Suppliers" into "Customers" (the columns that are not filled with data, will contain NULL):

### Example

INSERT  INTO  Customers (CustomerName,  City, Country)  
SELECT  SupplierName, City, Country  FROM  Suppliers;


The following SQL statement copies "Suppliers" into "Customers" (fill all columns):

### Example

INSERT  INTO  Customers (CustomerName, ContactName, Address, City, PostalCode,  Country)  
SELECT  SupplierName, ContactName, Address, City, PostalCode,  Country  FROM  Suppliers;


The following SQL statement copies only the German suppliers into "Customers":

### Example

INSERT  INTO  Customers (CustomerName,  City, Country)  
SELECT  SupplierName, City, Country  FROM  Suppliers  
WHERE  Country='Germany';

## The SQL CASE Statement

The CASE statement goes through conditions and return a value when the first condition is met (like an IF-THEN-ELSE statement). So, once a condition is true, it will stop reading and return the result. If no conditions are true, it returns the value in the ELSE clause.

If there is no ELSE part and no conditions are true, it returns NULL.

## CASE Syntax

CASE  
WHEN  _condition1_  THEN  _result1_  
WHEN  _condition2_  THEN  _result2_  
WHEN  _conditionN_  THEN  _resultN_  
ELSE  _result_  
END;


## SQL CASE Examples

The following SQL goes through conditions and returns a value when the first condition is met:

### Example

SELECT  OrderID, Quantity,  
CASE  
WHEN  Quantity >  30  THEN  "The quantity is greater than 30"  
WHEN  Quantity =  30  THEN  "The quantity is 30"  
ELSE  "The quantity is under 30"  
END  AS  QuantityText  
FROM  OrderDetails;



The following SQL will order the customers by City. However, if City is NULL, then order by Country:

### Example

SELECT  CustomerName, City, Country  
FROM  Customers  
ORDER  BY  
(CASE  
WHEN  City  IS  NULL  THEN  Country  
ELSE  City  
END);
## SQL IFNULL(), ISNULL(), COALESCE(), and NVL() Functions

Look at the following "Products" table:
Suppose that the "UnitsOnOrder" column is optional, and may contain NULL values.

Look at the following SELECT statement:

SELECT  ProductName, UnitPrice * (UnitsInStock + UnitsOnOrder)  
FROM  Products;

In the example above, if any of the "UnitsOnOrder" values are NULL, the result will be NULL.
## Solutions

**MySQL**

The MySQL  IFNULL()  function lets you return an alternative value if an expression is NULL:

SELECT  ProductName, UnitPrice * (UnitsInStock + IFNULL(UnitsOnOrder,  0))  
FROM  Products

or we can use the  COALESCE() function, like this:

SELECT  ProductName, UnitPrice * (UnitsInStock +  COALESCE(UnitsOnOrder,  0))  
FROM  Products

**SQL Server**

The SQL Server  ISNULL()function lets you return an alternative value when an expression is NULL:

SELECT  ProductName, UnitPrice * (UnitsInStock + ISNULL(UnitsOnOrder,  0))  
FROM  Products
## What is a Stored Procedure?

A stored procedure is a prepared SQL code that you can save, so the code can be reused over and over again.

So if you have an SQL query that you write over and over again, save it as a stored procedure, and then just call it to execute it.

You can also pass parameters to a stored procedure, so that the stored procedure can act based on the parameter value(s) that is passed.

### Stored Procedure Syntax

CREATE  PROCEDURE  _procedure_name_  
AS  
_sql_statement_  
GO;

### Execute a Stored Procedure

EXEC  _procedure_name_;
## Stored Procedure Example

The following SQL statement creates a stored procedure named "SelectAllCustomers" that selects all records from the "Customers" table:

### Example

CREATE  PROCEDURE  SelectAllCustomers  
AS  
SELECT  *  FROM  Customers  
GO;

Execute the stored procedure above as follows:

### Example

EXEC  SelectAllCustomers;
## Stored Procedure With One Parameter

The following SQL statement creates a stored procedure that selects Customers from a particular City from the "Customers" table:

### Example

CREATE  PROCEDURE  SelectAllCustomers  @City nvarchar(30)  
AS  
SELECT  *  FROM  Customers  WHERE  City = @City  
GO;

Execute the stored procedure above as follows:

### Example

EXEC  SelectAllCustomers City =  "London";

----------

## Stored Procedure With Multiple Parameters

Setting up multiple parameters is very easy. Just list each parameter and the data type separated by a comma as shown below.

The following SQL statement creates a stored procedure that selects Customers from a particular City with a particular PostalCode from the "Customers" table:

### Example

CREATE  PROCEDURE  SelectAllCustomers  @City nvarchar(30), @PostalCode nvarchar(10)  
AS  
SELECT  *  FROM  Customers  WHERE  City = @City  AND  PostalCode = @PostalCode  
GO;

Execute the stored procedure above as follows:

### Example

EXEC  SelectAllCustomers City =  "London", PostalCode =  "WA1 1DP";

## The SQL UNION Operator

The UNION operator is used to combine the result-set of two or more SELECT statements.

-   Each SELECT statement within UNION must have the same number of columns
-   The columns must also have similar data types
-   The columns in each SELECT statement must also be in the same order

### UNION Syntax

SELECT  _column_name(s)_  FROM  _table1_  
UNION  
SELECT  _column_name(s)_  FROM  _table2_;

### UNION ALL Syntax

The UNION operator selects only distinct values by default. To allow duplicate values, use UNION ALL:

SELECT  _column_name(s)_  FROM  _table1_  
UNION  ALL  
SELECT  _column_name(s)_  FROM  _table2_;

**Note:**  The column names in the result-set are usually equal to the column names in the first SELECT statement in the UNION.

## SQL UNION Example

The following SQL statement returns the cities (only distinct values) from both the "Customers" and the "Suppliers" table:

### Example

SELECT  City  FROM  Customers  
UNION  
SELECT  City  FROM  Suppliers  
ORDER  BY  City;


**Note:**  If some customers or suppliers have the same city, each city will only be listed once, because UNION selects only distinct values. Use UNION ALL to also select duplicate values!

----------

## SQL UNION ALL Example

The following SQL statement returns the cities (duplicate values also) from both the "Customers" and the "Suppliers" table:

### Example

SELECT  City  FROM  Customers  
UNION  ALL  
SELECT  City  FROM  Suppliers  
ORDER  BY  City;

## Different Types of SQL JOINs

Here are the different types of the JOINs in SQL:

-   **(INNER) JOIN**: Returns records that have matching values in both tables
-   **LEFT (OUTER) JOIN**: Return all records from the left table, and the matched records from the right table
-   **RIGHT (OUTER) JOIN**: Return all records from the right table, and the matched records from the left table
-   **FULL (OUTER) JOIN**: Return all records when there is a match in either left or right table
## SQL INNER JOIN Keyword

The INNER JOIN keyword selects records that have matching values in both tables.

### INNER JOIN Syntax

SELECT  _column_name(s)_  
FROM  _table1_  
INNER  JOIN  _table2  
_ON  _table1.column_name_ = _table2.column_name_;
## SQL INNER JOIN Example

The following SQL statement selects all orders with customer information:

### Example

SELECT  Orders.OrderID, Customers.CustomerName  
FROM  Orders  
INNER  JOIN  Customers  ON  Orders.CustomerID = Customers.CustomerID;


**Note:**  The INNER JOIN keyword selects all rows from both tables as long as there is a match between the columns. If there are records in the "Orders" table that do not have matches in "Customers", these orders will not be shown!
## JOIN Three Tables

The following SQL statement selects all orders with customer and shipper information:

### Example

SELECT  Orders.OrderID, Customers.CustomerName, Shippers.ShipperName  
FROM  ((Orders  
INNER  JOIN  Customers  ON  Orders.CustomerID = Customers.CustomerID)  
INNER  JOIN  Shippers  ON  Orders.ShipperID = Shippers.ShipperID);
## SQL FULL OUTER JOIN Keyword

The FULL OUTER JOIN keyword return all records when there is a match in either left (table1) or right (table2) table records.

**Note:**  FULL OUTER JOIN can potentially return very large result-sets!

### FULL OUTER JOIN Syntax

SELECT  _column_name(s)_  
FROM  _table1_  
FULL  OUTER  JOIN  _table2  
_ON  _table1.column_name_ = _table2.column_name_;

## SQL FULL OUTER JOIN Example

The following SQL statement selects all customers, and all orders:

SELECT  Customers.CustomerName, Orders.OrderID  
FROM  Customers  
FULL  OUTER  JOIN  Orders  ON  Customers.CustomerID=Orders.CustomerID  
ORDER  BY  Customers.CustomerName;

## SQL Self JOIN

A self JOIN is a regular join, but the table is joined with itself.

### Self JOIN Syntax

SELECT  _column_name(s)_  
FROM  _table1 T1, table1 T2_  
WHERE  _condition_;

## SQL Self JOIN Example

The following SQL statement matches customers that are from the same city:

### Example

SELECT  A.CustomerName  AS  CustomerName1, B.CustomerName  AS  CustomerName2,  A.City  
FROM  Customers A, Customers B  
WHERE  A.CustomerID <> B.CustomerID  
AND  A.City = B.City  
ORDER  BY  A.City;

