# Découverte de [SQLBolt](https://sqlbolt.com/)

## SQL, or Structured Query Language
is a language designed to allow both technical and non-technical users query, manipulate, and transform data from a relational database. 
And due to its simplicity, SQL databases provide safe and scalable storage for millions of websites and mobile applications.


### Did you know?
There are many popular SQL databases including SQLite, MySQL, Postgres, Oracle and Microsoft SQL Server. All of them support the common SQL language standard, which is what this site will be teaching, but each implementation can differ in the additional features and storage types it supports.

## Relational databases
 A relational database represents a collection of related (two-dimensional) tables. Each of the tables are similar to an Excel spreadsheet, with a fixed number of named columns (the attributes or properties of the table) and any number of rows of data.

## SQL Lesson 1: SELECT queries 101
### Select query for a specific columns
```sql
SELECT column, another_column, …
FROM mytable;
```

### Select query for all columns
```sql
SELECT * 
FROM mytable;
```

#### Ex 1 - Tasks
1. Find the *title* if each film
```sql
SELECT Title FROM movies;
```

2. Find the *director* if each film
```sql
SELECT Director FROM movies;
```

3. Find the *title* and *director* of each film
```sql
SELECT Title, Director FROM movies;
```

4. Find th *title* and *year* of each film
```sql
SELECT Title, Year FROM movies;
```

5. Find *all* the information about each film
```sql
SELECT * FROM movies;
```

## SQL Lesson 2: Queries with constraints (Pt. 1) 
### Select query with constraints
```sql
SELECT column, another_column, …
FROM mytable
WHERE condition
    AND/OR another_condition
    AND/OR …;
```

#### Ex 2 - Tasks
1. Find the movie with a row *id* of 6
```sql
SELECT * FROM movies WHERE id==6;
```

2. Find the movies released in the *years* between 2000 and 2010
```sql
SELECT * FROM movies WHERE year BETWEEN 2000 AND 2010;
```

3. Find the movies *not* released in the *years* between 2000 and 2010 
```sql
SELECT * FROM movies WHERE year NOT BETWEEN 2000 AND 2010;
```

4. Find the first 5 Pixar movies and their release *year*
```sql
SELECT * FROM movies WHERE id<=5;
```

#### Ex 3 - Tasks
1. Find all the Toy Story movies 
```sql
SELECT * FROM movies WHERE Title LIKE "Toy Story%";
```

2. Find all the movies directed by John Lasseter 
```sql
SELECT * FROM movies WHERE Director="John Lasseter";
```

3. Find all the movies (and director) not directed by John Lasseter 
```sql
SELECT * FROM movies WHERE Director!="John Lasseter";
```

4. Find all the WALL-* movies
```sql
SELECT * FROM movies WHERE Title LIKE "WALL%";
```

#### Ex 4 - Tasks
1. List all directors of Pixar movies (alphabetically), without duplicates 
```sql
SELECT DISTINCT Director FROM movies ORDER BY Director;
```

2. List the last four Pixar movies released (ordered from most recent to least)
```sql
SELECT * FROM movies ORDER BY Year DESC LIMIT 4;
```

3. List the first five Pixar movies sorted alphabetically 
```sql
SELECT * FROM movies ORDER BY Title LIMIT 5;
```

4. List the next five Pixar movies sorted alphabetically 
```sql
SELECT * FROM movies ORDER BY Title LIMIT 5 OFFSET 5;
```

#### Review 1 - Tasks
1. List all the Canadian cities and their populations
```sql
SELECT * FROM north_american_cities WHERE Country="Canada";
```

2. Order all the cities in the United States by their latitude from north to south 
```sql
SELECT * FROM north_american_cities WHERE Country="United States" ORDER BY Latitude DESC;
```

3. List all the cities west of Chicago, ordered from west to east 
```sql
SELECT * FROM north_american_cities WHERE Longitude < (Select Longitude from north_american_cities WHERE City="Chicago") ORDER BY Longitude ;
```

4. List the two largest cities in Mexico (by population)
```sql
SELECT * FROM north_american_cities WHERE Country="Mexico" ORDER BY Population DESC LIMIT 2;
```

5. List the third and fourth largest cities (by population) in the United States and their population 
```sql
SELECT * FROM north_american_cities WHERE Country="United States" ORDER BY Population DESC LIMIT 2 OFFSET 2;
```

#### Exercise 6 - Tasks
1. Find the domestic and international sales for each movie 
```sql
SELECT * FROM movies JOIN Boxoffice ON Id=Movie_id;
```

2. Show the sales numbers for each movie that did better internationally rather than domestically 
```sql
SELECT * FROM movies JOIN Boxoffice ON Id=Movie_id WHERE Domestic_sales<International_sales ORDER BY Domestic_sales;
```

3. List all the movies by their ratings in descending order 
```sql
SELECT * FROM movies JOIN Boxoffice ON Id=Movie_id ORDER BY Rating DESC;
```


#### Exercise 7 - Tasks
1. Find the list of all buildings that have employees 
```sql
Select * from Buildings JOIN Employees ON Building_name=Building GROUP BY Building_name;
```

2. Find the list of all buildings and their capacity 
```sql
Select * from Buildings;
```

3. List all buildings and the distinct employee roles in each building (including empty buildings) 
```sql
SELECT DISTINCT Role, Building_name FROM Buildings LEFT JOIN Employees ON Building_name = Building;
```


#### Exercise 8 - Tasks
1. Find the name and role of all employees who have not been assigned to a building 
```sql
SELECT Name, Role FROM employees WHERE Building IS NULL;
```

2. Find the names of the buildings that hold no employees 
```sql
SELECT * FROM Buildings LEFT JOIN Employees ON Building_name=Building WHERE NAME IS NULL;
```

#### Exercise 9 - Tasks
1. List all movies and their combined sales in millions of dollars 
```sql
SELECT Title, (Domestic_sales+International_sales)/1000000 as millions FROM movies join Boxoffice ON Id=Movie_Id;
```

2. List all movies and their ratings in percent
```sql
SELECT Title, (Rating)*10 as rating_per_cent FROM movies join Boxoffice ON Id=Movie_Id;
```

3. List all movies that were released on even number years 
```sql
SELECT * FROM movies join Boxoffice ON Id=Movie_Id WHERE YEAR%2=0;
```

#### Exercise 10 - Tasks
1. Find the longest time that an employee has been at the studio 
```sql
SELECT Building,MAX(Years_employed) FROM employees Group by building;
```

2. For each role, find the average number of years employed by employees in that role 
```sql
SELECT *,AVG(Years_employed) FROM employees Group by Role;
```

3. Find the total number of employee years worked in each building 
```sql
SELECT Building, SUM(Years_employed) FROM employees Group by building;
```

#### Exercise 11 - Tasks
1. Find the number of Artists in the studio (without a HAVING clause) 
```sql
SELECT count(name) FROM employees Group by artist;
```

2. Find the number of Employees of each role in the studio 
```sql
SELECT count(name) as nbEmployees, role FRom employees group by role;
```

3. Find the total number of years employed by all Engineers 
```sql
SELECT sum(years_employed) FROM employees where role="Engineer";
```

jusqu'à exercice 12