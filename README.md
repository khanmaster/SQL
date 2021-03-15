# SQL
```

--Database--
-- Get a list of database--
-- SELECT [NAME] FROM says.databases
-- Go

-- creating a database

CREATE DATABASE shahrukh_db;
-- click run
-- delete db

-- DROP DATABASE shahrukh_db;

-- let's use the db we created
USE shahrukh_db;

-- Let's create a table in our db

CREATE TABLE film_table
(
    -- FIRST IN IDENDITITY DENOTES THE START 
    -- 2ND DEGIT IN IDENTITY DENOTES TO INCREMENT
    film_ID INT IDENTITY(1,1) PRIMARY KEY,
    film_name VARCHAR(16),
    film_type VARCHAR(7)

)

-- LET'S CHECK IF THE TABLE HAS BEEN CREATED?
SP_HELP film_table
-- SP_HELP displays the structure of the table, not the data held inside it. 

-- lETS INSERT DATA INTO OUR TABLE
INSERT INTO film_table
VALUES
('Batman', 'Action'),
('Superman', 'Action')

-- NOW LETS FETCH THE DATA THAT WE INSERTED
SELECT * FROM film_table

-- LETS DO THIS WITH MORE FLEXIBILITY
INSERT INTO film_table
```
