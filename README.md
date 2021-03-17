# INTRODUCTION TO DATABASE
## SQL


- Establishing Database
- Get a list of databases
```
SELECT [NAME] FROM says.databases
```


- Creating a database

CREATE DATABASE shahrukh_db;
-- click run

- delete db
```
DROP DATABASE shahrukh_db;
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
- Let's see how can we sort the data
- WE CAN SORT THE DATA IN ASCENDING ORDER AND DESCENDING 
- BY DEFAULT THE DATA IS SORTED BY ASC ORDER 

```
SELECT UnitPrice, Quantity, Discount, UnitPrice*Quantity AS 'Gross Total' FROM [Order Details] ORDER BY 'GROSS TOTAL' DESC    
SELECT TOP 5 UnitPrice, Quantity, Discount, UnitPrice * Quantity AS 'Gross Total'
FROM [Order Details]
ORDER BY 'Gross Total' ASC
```
```
SELECT PostalCode 'Post Code', LEFT(PostalCode, CHARINDEX(' ',PostalCode)-1) AS 'Post Code Region' CHARINDEX(' ',PostalCode) AS 'space found',
Country
FROM Customers WHERE Country = 'UK'
```
```
SELECT PostalCode “Post Code”,
LEFT(PostalCode, CHARINDEX(‘ ‘,PostalCode)-1) AS “Post Code Region”,
CHARINDEX(‘ ‘,PostalCode) AS ”Space Found”, Country
FROM Customers
WHERE Country = ‘UK’

SELECT * FROM Customers
```
```
SELECT PostalCode 'Post Code',
LEFT(PostalCode, CHARINDEX(' ',PostalCode)) AS 'Post Code Region',
CHARINDEX(' ',PostalCode) AS 'Space Found at Character', Country
FROM Customers
WHERE Country = 'UK'
```

- What is an apostroh
```
SELECT ProductName, CHARINDEX('''', Products.ProductName) AS "Apostrophe Found" FROM Products WHERE
```
- Date functions
```
SELECT DATEADD(d,5,OrderDate) AS "Due Date", DATEDIFF(d,OrderDate,ShippedDate) AS "Ship days" From Orders
```
- DATEADD has 3 arguments 
- d or dd means day, m or mm month, yy or yyyy year
- The Date to be added to
- How many units to add

- DATEDIFF uses the same datepart argument abbreviations followed by the two dates for the calculation.
```
SELECT FORMAT(Orders.OrderDate,5) FROM Orders
```

- Output a list of Employees from the Employees table including their Name (concatenated) and their Age (calculated from BirthDate)
```
SELECT e.FirstName +' '+e.LastName AS "Employee Name",
DATEDIFF(YY, BirthDate, GETDATE()) AS "AGE"
FROM Employees e
```
- CASE statements can be useful when you need varying results output based on differing data.

- Pay close attention to WHEN THEN ELSE and END

- Use single quotes for data and double quotes for column aliases.

```
SELECT CASE
WHEN DATEDIFF(d,OrderDate,ShippedDate) < 10 THEN 'On Time'
ELSE 'Overdue' -- single quotes for data
END AS "Status" -- using double quotes for column
FROM Orders
```
- Use CASE to add a column to the previous activity solution called Retirement Status as follows:

- Age greater than 65 = ”Retired”
- Age greater than 60 = “Retirement due”
- Age less than 60 = “More than 5 years to go”
```
SELECT CASE 
WHEN DATEDIFF(YY, e.BirthDate, GETDATE()) > 65 THEN 'Retired'
WHEN DATEDIFF(YY, e.BirthDate, GETDATE()) > 60 THEN 'Retired Due'
ELSE 'MORE THAN 5 YEARS LEFT'
END AS "EMPLOYEMENT STATUS"
FROM Employees e
```
- link to the northwind Diagram
- https://docs.yugabyte.com/latest/sample-data/northwind/
```
CREATE DATABASE shahrukh_db
USE shahrukh_db

DROP TABLE IF EXISTS course
CREATE TABLE course  
(
    c_id INT IDENTITY(1,1) PRIMARY KEY,
    course_name VARCHAR(30)
)

DROP TABLE IF EXISTS student
CREATE TABLE student
(
    st_id INT IDENTITY(1,1),
    student_name VARCHAR(30),
    course_id INT,
    FOREIGN KEY (course_id) REFERENCES course(c_id) ON DELETE CASCADE

)
```
```
INSERT INTO course
(
    course_name
)
VALUES
(
    'Business' 
),
(
    'Test'
),
(
    'Agile'
),
(
    'Web'
),
(
    'Dev'
)
```
```
INSERT INTO student
(
   student_name, course_id 
)
VALUES
(
    'Lee', 1
),
(
    'Barry', 1
),
(
    'David', 2
),
(
    'Tim',5
)


INSERT INTO student
(
   student_name
)
VALUES
(
    'Nicole'   
)

SELECT * FROM student
SELECT * FROM course
```
- /*INNER JOIN-matched rows*/
- --DOD-->JOIN SYNTAX-->1. Applying the join keyword based on the question
                -->2. Understanding which table to put in the left and which at the right
                -->3. Applying the ON keyword to define the primary key and foreign key relationship

```
SELECT * FROM student s INNER JOIN course c
ON s.course_id=c.c_id --ON defines primary key and foeign key relationship
```
- /*OUTER JOINS-LEFT JOIN, RIGHT JOIN, FULL JOIN*/
- /*LEFT JOIN-All the rows from the left table and only the matching rows from the right table*/
```
SELECT * FROM student s LEFT JOIN course c   
ON s.course_id=c.c_id

SELECT * FROM student s RIGHT JOIN  course c
ON s.course_id=c.c_id

SELECT * FROM student s FULL JOIN course c   
ON s.course_id=c.c_id


SELECT * FROM Products
```
```
USE Northwind 
```
- SELECT OrdersID, CONVERT(varchar(10,OrderDate,103))

- SUB QUERY SYNTAX
```
SELECT CompanyName AS "Customer" FROM Customers
WHERE CustomerID Not in (SELECT CustomerID FROM Orders)
```
- LETS USE JOINS TO GET THE SAME RESULTS
```

SELECT c.CompanyName AS 'Customer'
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID
WHERE OrderID IS NULL
```
- another example of sub query as nested query here SELECT CLAUSE acts as a column
```
SELECT OrderID, ProductID, UnitPrice, Quantity, Discount,
(SELECT MAX(UnitPrice)From [Order Details] od) AS "Max Price"
From [Order Details]
```

- sub query using a table
```
SELECT od.ProductID, sq1.totalamt AS "total sold for this product",
UnitPrice, UnitPrice/totalamt*100 AS "% of Total"
FROM [Order Details] od 
INNER JOIN
(SELECT ProductID, SUM(UnitPrice * Quantity) AS totalamt
FROM [Order Details] GROUP BY ProductID) sq1 ON sq1.ProductID = od.ProductID 
```
- Using a Subquery in the WHERE clause, list all Orders
- (Order ID, Product ID, Unit Price, Quantity and Discount)
- from the [Order Details] table where the product has been discontinued

- Now repeat the same exercise using a simple join
```
SELECT OrderID, UnitPrice, Quantity, Discount 
FROM [Order Details]
WHERE ProductID IN 
(SELECT ProductID FROM Products WHERE Discontinued = 1);
```
- Lets try this with joins
```
SELECT od.OrderID, p.UnitPrice, od.Quantity, od.Discount FROM [Order Details] od

INNER JOIN [Products] p ON od.ProductID = p.ProductID

WHERE p.Discontinued = 1
```

- Keeping code clearn
```
SELECT od.OrderID, p.ProductID, od.UnitPrice, od.Quantity, od.Discount FROM [Order Details] od

INNER JOIN [Products] p ON p.ProductID = od.ProductID 

WHERE p.Discontinued = 1
```

- UNION ALL returns all 28 tows
- UNION removes any duplicates
```
SELECT e.Employeeid AS "Employee/Supplier" From Employees e
UNION ALL
SELECT SupplierID FROM Suppliers 
```
- UNION removes any duplicates
```
SELECT e.Employeeid AS "Employee/Supplier" From Employees e UNION SELECT SupplierID FROM 
Suppliers
```
