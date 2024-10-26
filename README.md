# SQL-SORTING AND GROUPING DATA
## INTRODUCTION
This project involves working with two tables, `Country` and `Persons`, in a relational database. The purpose is to practice data insertion, querying, sorting, grouping, and various SQL functions through a series of tasks.
## TABLE STRUCTURES
### Country Table Structure
* Id: INT (Primary Key) – Unique identifier for each country.
* Country_name: VARCHAR(50) – Name of the country.
* Population: BIGINT – Population of the country.
* Area: INT – Area
### Persons Table Structure
* Id: INT (Primary Key) – Unique identifier for each person.
* Fname: VARCHAR(50) – First name of the person.
* Lname: VARCHAR(50) – Last name of the person.
* Population: BIGINT – Population of the person’s country.
* Rating: DECIMAL – Rating of the person .
* Country_Id: INT (Foreign Key) – References the Id field in the Country table.
* Country_name: VARCHAR(50) – Name of person’s country.
## TASKS
Insert 10 rows into both tables, as given below. Create a table named Country with fields: Id Country_name Population Area Create another table named Persons with fields: Id Fname Lname Population Rating Country_Id Country_name
1. Write an SQL query to print the first three characters of Country_name from the Country table.
2. Write an SQL query to concatenate first name and last name from Persons table.
3.  Write an SQL query to count the number of unique country names from Persons table.
4. Write a query to print the maximum population from the Country table.
5. Write a query to print the minimum population from Persons table.
6. Insert 2 new rows to the Persons table making the Lname NULL. Then write another query to count Lname from Persons table.
7. Write a query to find the number of rows in the Persons table.
8. Write an SQL query to show the population of the Country table for the first 3 rows. (Hint: Use LIMIT)
9. Write a query to print 3 random rows of countries. (Hint: Use rand() function and LIMIT)
10. List all persons ordered by their rating in descending order.
11. Find the total population for each country in the Persons table.
12. Find countries in the Persons table with a total population greater than 50,000
13. List the total number of persons and average rating for each country, but only for countries with more than 2 persons, ordered by the average rating in ascending order
## QUERIES
#### Create Country table with fields: Id ,Country_name ,Population & Area 
```sql
CREATE TABLE Country (
    Id INT PRIMARY KEY,
    Country_name VARCHAR(50),
    Population BIGINT,
    Area INT
);
DESC country;
```
#### Create persons table with fields: Id ,Fname, Lname, Population, Rating ,Country_Id & Country_name.
```sql
CREATE TABLE Persons (
    Id INT PRIMARY KEY,
    Fname VARCHAR(50),
    Lname VARCHAR(50),
    Population BIGINT,
    Rating DECIMAL(3, 2),
    Country_Id INT,
    Country_name VARCHAR(50),
    FOREIGN KEY (Country_Id) REFERENCES Country(Id)
);
DESC persons;
```
#### Insert data into Country table
```sql
INSERT INTO Country (Id, Country_name, Population, Area)
VALUES 
(1, 'USA', 75000000, 9833520),
(2, 'India', 5000000, 3287263),
(3, 'Canada', 8000000, 9984670),
(4, 'UK', 150000000, 243610),
(5, 'Australia', 400000, 7692024),
(6, 'Germany', 2000000, 357022),
(7, 'France', 6900000, 551695),
(8, 'Brazil', 6000000, 8515767),
(9, 'Russia', 15500000, 17098242),
(10, 'Japan', 8650000, 377930);

select * from country;
```
#### Insert data into Persons table
```sql
INSERT INTO Persons (Id, Fname, Lname, Population, Rating, Country_Id, Country_name)
VALUES
(1, 'Jeeva', 'Joseph', 75000000, 4.5, 1, 'USA'),
(2, 'Arya', 'Shan', 5000000, 3.8, 2, 'India'),
(3, 'Emma', 'Emmi', 8000000, 4.9, 3, 'Canada'),
(4, 'Basim', 'Johny', 150000000, 4.2, 4, 'UK'),
(5, 'Aryan', 'John', 400000, 3.9, 5, 'Australia'),
(6, 'Maria', 'Grace', 2000000, 4.7, 6, 'Germany'),
(7, 'James', 'Wilson', 6900000, 2.1, 7, 'France'),
(8, 'Suzzy', 'Martin', 6000000, 4.0, 8, 'Brazil'),
(9, 'Robert', 'Williams', 15500000, 1.7, 9, 'Russia'),
(10, 'Jane', 'Taylor', 8650000, 4.6, 10, 'Japan');
select * from persons;
```
 #### (1) Write an SQL query to print the first three characters of Country_name from the Country table. 
 ```sql
SELECT LEFT(Country_name, 3) AS First_Three_Chars FROM Country;
```
#### (2) Write an SQL query to concatenate first name and last name from Persons table.
```sql
SELECT CONCAT(Fname, ' ', Lname) AS Full_Name FROM Persons;
```
#### (3) Write an SQL query to count the number of unique country names from Persons table. 
```sql
SELECT COUNT(DISTINCT Country_Id) AS Unique_Country_Names FROM Persons;
```
#### (4) Write a query to print the maximum population from the Country table. 
```sql
SELECT MAX(Population) AS Maximum_Population FROM Country;
```
#### (5) Write a query to print the minimum population from Persons table.
```sql
SELECT MIN(Population) AS Minimum_Population FROM Country;
```
#### (6) Insert 2 new rows to the Persons table making the Lname NULL. Then write another query to count Lname from Persons table.
```sql
INSERT INTO Persons (Id, Fname, Lname, Population, Rating, Country_Id,Country_name) VALUES
(11, 'Aishwarya', NULL,75000000, 4.5, 1, 'USA'),
(12, 'Daisyy', NULL, 15500000, 1.7, 9, 'Russia');
SELECT * FROM persons;
SELECT COUNT(Lname) AS Count_of_Lnames FROM Persons;
```
#### (7) Write a query to find the number of rows in the Persons table. 
```sql
SELECT COUNT(*) AS Total_Rows FROM Persons;
```
#### (8) Write an SQL query to show the population of the Country table for the first 3 rows. (Hint: Use LIMIT) 
```sql
SELECT Population FROM Country LIMIT 3;
```
#### (9) Write a query to print 3 random rows of countries. (Hint: Use rand() function and LIMIT) 
```sql
SELECT * FROM Country ORDER BY RAND() LIMIT 3;
```
#### (10) List all persons ordered by their rating in descending order. 
```sql
SELECT * FROM Persons ORDER BY Rating DESC;
```
 #### (11)Find the total population for each country in the Persons table. 
 ```sql
SELECT Country_name, SUM(Population) AS Total_Population FROM Persons GROUP BY Country_name;
```
 #### (12) Find countries in the Persons table with a total population greater than 50,000
```sql
SELECT Country_name FROM Persons GROUP BY Country_name HAVING SUM(Population) > 50000;
```
#### (13) List the total number of persons and average rating for each country, but only for countries with more than 2 persons, ordered by the average rating in ascending order
```sql
SELECT Country_name, COUNT(Id) AS Total_no_of_Persons, AVG(Rating) AS Average_Rating
FROM Persons
GROUP BY Country_name
HAVING COUNT(Id) >2
ORDER BY Average_Rating ASC;
```
#### List the total number of persons and average rating for each country, but only for countries with  2 or more persons, ordered by the average rating in ascending order
```sql
SELECT Country_name, COUNT(Id) AS Total_no_of_Persons, AVG(Rating) AS Average_Rating
FROM Persons
GROUP BY Country_name
HAVING COUNT(Id) >=2
ORDER BY Average_Rating asc;
```
## CONCLUSION
This project provides practical SQL query examples to manage and analyze data within a relational database. By using SQL commands, this project demonstrates essential techniques for filtering, sorting, grouping, and aggregating data. 
