# INTRODUCTION TO DATABASE
## SQL
```

--Database--
-- Get a list of database--
-- SELECT [NAME] FROM says.databases
-- Go
```

- creating a database
```
CREATE DATABASE shahrukh_db;
-- click run
```
- DELETE DB
```SQL
-- delete db

-- DROP DATABASE shahrukh_db;
```

- Let's use the db we created
```
USE shahrukh_db;
```
- Let's create a table in our db
```
CREATE TABLE film_table
(
    -- FIRST IN IDENDITITY DENOTES THE START 
    -- 2ND DEGIT IN IDENTITY DENOTES TO INCREMENT
    film_ID INT IDENTITY(1,1) PRIMARY KEY,
    film_name VARCHAR(16),
    film_type VARCHAR(7)

)
```
- LET'S CHECK IF THE TABLE HAS BEEN CREATED?
```
SP_HELP film_table
```
- SP_HELP displays the structure of the table, not the data held inside it. 

- lETS INSERT DATA INTO OUR TABLE
```
INSERT INTO film_table
VALUES
('Batman', 'Action'),
('Superman', 'Action')
```
- NOW LETS FETCH THE DATA THAT WE INSERTED
```
SELECT * FROM film_table
```
- LETS DO THIS WITH MORE FLEXIBILITY
```
INSERT INTO film_table
```

- NOW LET'S ALTER OUR TABLE AND USE NOT NULL
```
ALTER TABLE film_table
ALTER COLUMN film_name VARCHAR(10) NOT NULL
```
- LETS DO THIS WITH MORE FLEXIBILITY
```
INSERT INTO film_table
(film_name)
VALUES
('notebook')
```
- PRACTICE MORE
```
SELECT * FROM film_table

ALTER TABLE film_table
ADD CONSTRAINT Default_SciFi DEFAULT 'Batman' FOR film_type
```
- INSERT INTO film_table
```
INSERT INTO film_table
(film_name)
VALUES
('start war4')
```
- Lets update data where film type is null

```
UPDATE film_table
SET film_type='Classic'
WHERE film_type is NULL
```
- Let's see how can we delete from our table
```
DELETE FROM film_table
WHERE film_type ='Action'

SP_HELP film_table

```
## QUERING NORTHWIND DB

```
### USING Northwind
- WE WILL CONNECT TO NORTHWIND as we already have data available to query 

- select from customers table using WHERE
```
SELECT * FROM Customers
WHERE Customers.City = 'Paris'
```
- LETS CREATE ALAISIS as we have nick name
- select from customers table using WHERE
```
SELECT * FROM Customers c
WHERE c.City = 'Paris'
```
- Let's solve the problems
- How many Employees have a home City of London?
```
SELECT COUNT(*) AS "HOW MANY EMPLOYEES LIVE IN LONDON" FROM Employees e
WHERE e.City = 'London'
```
- CONTCATEMATION AND COLUM ALIASING 
```
SELECT e.FirstName + ' ' + LastName AS "NAME OF EMPLOYEES FROM LONDON AREA" FROM Employees e
WHERE e.City = 'London'
```

- LETS USE AGGREGATE How many Employees have a home City of London?
```
SELECT * FROM Employees e
WHERE e.City = 'London'
```
- Which Employee is a Doctor?
```
SELECT * FROM Employees e
WHERE e.TitleOfCourtesy = 'Dr.'
```
- How many Products are discontinued?
```
SELECT * FROM Products p
WHERE p.Discontinued = 1
```
- LETS SEE HOW CAN WE COUNT
- How many Products are discontinued?
```
SELECT COUNT(*) AS "NUMBER OF PRODUCTS" FROM Products p
WHERE p.Discontinued = 1
```
- Lets see how should we structure our queries

- TOP 10, company names form customers TABLE
```
SELECT TOP 10 CompanyName, City FROM Customers
WHERE Country = 'France'
```
- Let's use AND key word to select 
```
SELECT ProductName, UnitPrice FROM Products
WHERE CategoryID = 1 AND Discontinued = 0
```
- Let's investigate data type
```
SP_HELP Products 
```
- Let's check stock on hand more than 0 with price range over 29.99 using AND keyword
```
SELECT ProductName, UnitPrice FROM Products
WHERE UnitsInStock > 0 AND UnitPrice > 29.99
```


- Let's check stock on hand more than 0 with price range over 29.99 using or keyword
```
SELECT ProductName, UnitPrice FROM Products
WHERE UnitsInStock > 0 OR UnitPrice > 29.99
```
- DISTINCT is used to remove duplicate values
```
SELECT DISTINCT Country FROM Customers
WHERE ContactTitle = 'Owner'
```
- What is a WILDCARDS in SQL
- use cases
```
SELECT * FROM Products p
```
- run it now and see products name
- now if we need to the names of products start from A
```
SELECT p.ProductName FROM Products p WHERE p.ProductName Like 'A%'
```
- if we would like to exclude anything from the result
```
SELECT P.ProductName FROM Products P WHERE p.ProductName LIKE '[^ACD]'
```
- THIS WILL REMOVE ANY PRODUCT NAME WHICH INCLUDE ACD
```
SELECT ProductName FROM Products WHERE ProductName LIKE 'ch%'
```
- this will result in all products starting with ch
```
SELECT * FROM Customers WHERE Region LIKE '_A'
```
- THIS HELP US FIND REGIONS ENDING WITH A - BEST EXAMPLE TO USE LIKE KEY WORD

- IF WE NEEDED TO FIND CUSTOMERS IN TWO SPECIFIC NAMED REGIONS USING IN KEYWROD
```
SELECT * FROM Customers WHERE Region IN ('WA','SP')
```
- LET'S SEE HOW CAN WE FIND TERRITORIES WITH ID RANGES
```
SELECT * FROM EmployeeTerritories WHERE TerritoryID BETWEEN 06800 AND 09999
```
- THIS WILL RESULT 3 ROWS AVAILABLE IN THE RANGE GIVEN


 ### Practice time

- Write queries to find out the following from Northwind:

- How many orders are there for EmployeeIDs 5 and 7 (The total for both)

- What are the names and product IDs of the products with a unit price below 5.00?
```
SELECT ProductName, ProductID FROM Products WHERE UnitPrice < 5.00 
```
- Which categories have a category name with initials beginning with B or S? 
```
SELECT CategoryName FROM Categories WHERE CategoryName LIKE 's%' OR CategoryName Like'b%'
```

- How many orders are there for EmployeeIDs 5 and 7 (The total for both)
```
SELECT EmployeeID FROM Orders o where EmployeeID = 5 or EmployeeID = 7
```
- lets use GROUPBY to solve this problem
```
SELECT EmployeeID FROM Orders WHERE EmployeeID IN (5,7) GROUP BY EmployeeID
```
-- another example of contatenation 
```
SELECT CompanyName AS 'Company Name', City + ',' + Country AS 'City' From Customers
```
- another way of writing it
- SELECT CompanyName AS 'Company Name', CONCAT (Customers.City, ',' Customers.Country) AS City From Customers

- FETCH THE COMAPANY NAME BY CITY AND COUNTRY WHERE REGION IS NULL 
```
SELECT CompanyName AS "Company Name", City + ',' + Country AS 'City' FROM Customers WHERE Region IS NULL
```

- Write a SELECT statement to list the six countries that have Region Codes in the Customers Table
```
SELECT DISTINCT COUNTRY FROM Customers WHERE Region IS NOT NULL 
```
- this is where DISTINT  key word come into play

- GETTING A GROSS TOTAL
```
SELECT UnitPrice, Quantity, Discount, UnitPrice * Quantity AS "Gross Total" FROM [Order Details] 
```
