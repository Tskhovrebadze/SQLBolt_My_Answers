# SQLBOLT Practice Project



_This is one of the best sources to learn SQL easily._

_You can improve your SQL skills from here: [SQLBolt](https://sqlbolt.com/)._

  

_**All of my answers in this project are based on exercises from this website.**_

  

---
# SQL Lesson 1: SELECT queries 101


>_We will be using a database with data about some of Pixar's classic movies for most of our exercises. This first exercise will only involve the Movies table. Alter the query to find the exact information we need for each task._

---

### Exercise 1 — Tasks

  

_**1.Find the title of each film**_


>SELECT Title FROM movies;
  
  ---
 

_**2.Find the director of each film**_


>SELECT Director FROM movies;

---

  

_**3.Find the title and director of each film**_



>SELECT Title, Director FROM movies;

---

  

_**4.Find the title and year of each film**_

>SELECT Title, Year FROM movies;

---

  

_**5.Find all the information about each film**_


>SELECT * FROM movies;

---

  

# SQL Lesson 2: Queries with constraints (Pt. 1)
___

>_Using the right constraints, find the information we need from the Movies table for each task below._

---

  

### Exercise 2 — Tasks

  

_**1.Find the movie with a row id of 6**_

>SELECT * FROM movies WHERE Id = 6;

---

  

_**2.Find the movies released in the years between 2000 and 2010**_


>SELECT * FROM movies WHERE Year BETWEEN 2000 AND 2010;

---

  

_**3.Find the movies not released in the years between 2000 and 2010**_


>SELECT * FROM movies WHERE Year NOT BETWEEN 2000 AND 2010;

---

  

_**4.Find the first 5 Pixar movies and their release year**_

>SELECT Title, Year FROM movies LIMIT 5;

---

  

# SQL Lesson 3: Queries with constraints (Pt. 2)

---

>_Here's the definition of a query with a WHERE clause again, go ahead and try and write some queries with the operators above to limit the results to the information we need in the tasks below._

---

  

### Exercise 3 — Tasks

  

_**1.Find all the Toy Story movies**_

>SELECT * FROM movies WHERE Title LIKE '%Toy Story%';

---

  

_**2.Find all the movies directed by John Lasseter**_

>SELECT * FROM movies WHERE Director = 'John Lasseter';

---

  

_**3.Find all the movies (and director) not directed by John Lasseter**_

>SELECT Title, Director FROM movies WHERE Director != 'John Lasseter';

---

  

_***4.Find all the WALL-****_ **movies**

>SELECT Title FROM movies WHERE Title LIKE '%WALL%';

---

  

# SQL Lesson 4: Filtering and sorting Query results

---

>_There are a few concepts in this lesson, but all are pretty straight-forward to apply.
To spice things up, we've scrambled the Movies table in the exercise to better mimic real-life data.
Try to use the necessary keywords and clauses introduced above in your queries._

---

  

### Exercise 4 — Tasks

  

_**1.List all directors of Pixar movies (alphabetically), without duplicates**_


>SELECT DISTINCT Director FROM movies ORDER BY Director;

---

_**2.List the last four Pixar movies released (ordered from most recent to least)**_


>SELECT Title FROM movies ORDER BY Year DESC LIMIT 4;

 --- 

_**3.List the first five Pixar movies sorted alphabetically**_


>SELECT Title FROM movies ORDER BY Title LIMIT  5;

  ---

_**4.List the next five Pixar movies sorted alphabetically**_


>SELECT Title FROM movies ORDER BY Title LIMIT 5 OFFSET 5;

  ---
  
# SQL Review: Simple SELECT Queries

---

>_Try and write some queries to find the information requested in the tasks below. You may have to use a different combination of clauses in your query for each task. Once you're done, continue onto the next lesson to learn about queries that span multiple tables._
---

  

### Review 1 — Tasks

  

_**1.List all the Canadian cities and their populations**_



>SELECT City, Population  FROM north_american_cities
>WHERE Country = 'Canada';

  ---

_**2.Order all the cities in the United States by their latitude from north to south**_

>SELECT City FROM north_american_cities
>WHERE Country = 'United States'
>ORDER BY Latitude DESC;

  ---

_**3.List all the cities west of Chicago, ordered from west to east**_


>SELECT City, Longitude FROM north_american_cities
>WHERE Longitude < -87.629798
>ORDER BY Longitude ASC;

 --- 

_**4.List the two largest cities in Mexico (by  population)**_


>SELECT City, Population FROM north_american_cities
>WHERE Country = 'Mexico'
>ORDER BY Population DESC
>LIMIT 2;

  
---
_**5.List the third and fourth largest cities (by population) in the United States and their population**_

>SELECT City, Population  FROM north_american_cities
>WHERE Country LIKE  'United States'
>ORDER BY  Population
>LIMIT  2 OFFSET 2;

  
  

# SQL Lesson 6: Multi-table queries with JOINs

---

>_We've added a new table to the Pixar database so that you can try practicing some joins. The BoxOffice table stores information about the ratings and sales of each particular Pixar movie, and the Movie_id column in that table corresponds with the Id column in the Movies table 1-to-1. Try and solve the tasks below using the INNER JOIN introduced above._

---

### Exercise 6 — Tasks

  

_**1.Find the domestic and international sales for each movie**_


>SELECT Title , Domestic_sales, International_sales FROM Movies
>INNER JOIN Boxoffice ON
>Boxoffice.Movie_id =  Movies.Id;
---
  

_**2.Show the sales numbers for each movie that did better internationally rather than domestically**_


>SELECT Title, Domestic_sales,International_sales FROM Movies
>INNER JOIN Boxoffice ON
>Movies.Id = Boxoffice.Movie_id
>WHERE International_sales > Domestic_sales;
----
  

_**3.List all the movies by their ratings in descending order**_


>SELECT Title, Rating FROM Movies
>INNER JOIN Boxoffice ON
>Movies.Id = Boxoffice.Movie_id
>ORDER BY Rating DESC;

  ---
  

# SQL Lesson 7: OUTER JOINs

---

  

>_In this exercise, you are going to be working with a new table which stores fictional data about Employees in the film studio and their assigned office Buildings. Some of the buildings are new, so they don't have any employees in them yet, but we need to find some information about them regardless._

---
>_Since our browser SQL  database  is somewhat limited, only the LEFT JOIN  is  supported  in the exercise below._

---

  

### Exercise 7 — Tasks

  

_**1.Find the list of all buildings that have employees**_

>SELECT DISTINCT Building FROM Employees;
>Find the list of all buildings and their capacity
>SELECT * FROM Buildings;
---
  

_**2.List all buildings and the distinct employee roles in each building (including empty buildings)**_

>SELECT DISTINCT Building_name, Role  FROM Buildings
>LEFT JOIN Employees ON Building_name = Building;
---
  
  

# SQL Lesson 8: A short note on  NULLs

---

>_This exercise will be a sort of review of the last few lessons. We're using the same Employees and Buildings table from the last lesson, but we've hired a few more people, who haven't yet been assigned a building._

---

  
  

### Exercise 8 — Tasks

  

_**1.Find the name and role of all employees who have not been assigned to a building**_

>SELECT Name,Role FROM employees WHERE Building IS NULL;

  ---

_**2.Find the names of the buildings that hold no employees**_

>SELECT DISTINCT Building_name FROM Buildings
>LEFT JOIN Employees ON Building_name = Building
>WHERE Role IS NULL;
---
  

# SQL Lesson 9: Queries with expressions**

---

>_You are going to have to use expressions to transform the BoxOffice data into something easier to understand for the tasks below._

---

  

### Exercise 9 — Tasks

  

_**1.List all movies and their combined sales in millions of dollars**_


>SELECT DISTINCT Title, (Domestic_sales + International_sales) / 1000000 AS Sales FROM Movies
>INNER JOIN Boxoffice ON
>Movies.Id = Boxoffice.Movie_id;

  ---

_**2.List all movies and their ratings in percent**_

>SELECT DISTINCT Title, (Rating * 10) AS Rating_Percent FROM Movies
>INNER JOIN Boxoffice ON
>Movies.Id = Boxoffice.Movie_id;

 --- 

_**3.List all movies that were released on even number years**_

>SELECT Title FROM Movies WHERE Year % 2 = 0;
---
  
  

# SQL Lesson 10: Queries with aggregates (Pt. 1)

---

>_For this exercise, we are going to work with our Employees table. Notice how the rows in this table have shared data, which will give us an opportunity to use aggregate functions to summarize some high-level metrics about the teams. Go ahead and give it a shot._

---

### Exercise 10 — Tasks

  

_**1.Find the longest time that an employee has been at the studio**_

>SELECT MAX(Years_employed) FROM employees;

---  

_**2.For each role, find the average number of years employed by employees in that role**_

>SELECT Role, AVG(Years_employed) AS Average_Years FROM Employees GROUP BY Role;

  

_**3.Find the total number of employee years worked in each building**_

>SELECT DISTINCT Building, SUM(Years_employed) FROM Employees
>GROUP BY Building;

  
  
---
# SQL Lesson 11: Queries with aggregates (Pt. 2)

---

>_For this exercise, you are going to dive deeper into Employee data at the film studio. Think about the different clauses you want to apply for each task._

---

### Exercise 11 — Tasks

  

_**1.Find the number of Artists in the studio (without a HAVING clause)**_

>SELECT COUNT(*) FROM Employees
>WHERE Role LIKE 'Artist';
---
  

_**2.Find the number of Employees of each role in the studio**_


>SELECT DISTINCT Role, COUNT(*) FROM Employees
>GROUP BY Role;

  

_**3.Find the total number of years employed by all Engineers.**

>SELECT Role, SUM(Years_employed) FROM Employees
>GROUP BY Role
>HAVING Role = 'Engineer';

  
---  
# SQL Review: Simple SELECT Queries

---

>_Try and write some queries to find the information requested in the tasks below. You may have to use a different combination of clauses in your query for each task. Once you're done, continue onto the next lesson to learn about queries that span multiple tables._

---

### Review 1 — Tasks

_**3. Find the total number of years employed by all Engineers.**_

> SELECT Role, SUM(Years_employed) FROM Employees  
> GROUP BY Role  
> HAVING Role = 'Engineer';

# SQL Lesson 12: Order of execution of a Query

---

>_Here ends our lessons on SELECT queries, congrats of making it this far! This exercise will try and test your understanding of queries, so don't be discouraged if you find them challenging. Just try your best._

---

### Exercise 12 — Tasks

_**1. Find the number of movies each director has directed.**_

> SELECT Director, COUNT(Title) AS Amount_of_Movies FROM Movies  
> GROUP BY Director;
----
_**2. Find the total domestic and international sales that can be attributed to each director.**_

> SELECT Director, SUM(Domestic_sales + International_sales) AS Sales FROM Movies  
> INNER JOIN Boxoffice ON Movies.Id = Boxoffice.Movie_id  
> GROUP BY Director;

# SQL Lesson 13: Inserting rows

---

>_In this exercise, we are going to play studio executive and add a few movies to the Movies to our portfolio. In this table, the Id is an auto-incrementing integer, so you can try inserting a row with only the other columns defined._
>_Since the following lessons will modify the database, you'll have to manually run each query once they are ready to go._

---

### Exercise 13 — Tasks

_**1. Add the studio's new production, Toy Story 4 to the list of movies (you can use any director).**_

> INSERT INTO Movies VALUES (4, 'Toy Story 4', 'John Lasseter', 2013, 100);
---
_**2. Toy Story 4 has been released to critical acclaim! It had a rating of 8.7, and made 340 million domestically and 270 million internationally. Add the record to the BoxOffice table.**_

> INSERT INTO Boxoffice VALUES (4, 8.7, 340000000, 270000000);

# SQL Lesson 14: Updating rows

---

>_It looks like some of the information in our Movies database might be incorrect, so go ahead and fix them through the exercises below._

---

### Exercise 14 — Tasks

_**1. The director for A Bug's Life is incorrect, it was actually directed by John Lasseter.**_

> UPDATE Movies  
> SET Director = 'John Lasseter'  
> WHERE Id = 2;
---
> UPDATE Movies  
> SET Director = 'John Lasseter'  
> WHERE Title = "A Bug's Life";

_**2. The year that Toy Story 2 was released is incorrect, it was actually released in 1999.**_

> UPDATE Movies  
> SET Year = '1999'  
> WHERE Title = 'Toy Story 2';
---
_**3.Both the title and director for Toy Story 8 is incorrect! The title should be "Toy Story 3" and it was directed by Lee Unkrich.**_

> UPDATE Movies  
> SET Title = 'Toy Story 3', Director = 'Lee Unkrich'  
> WHERE Movies.Id = 11;

# SQL Lesson 15: Deleting rows

---

>_The database needs to be cleaned up a little bit, so try and delete a few rows in the tasks below._

---

### Exercise 15 — Tasks

_**1. This database is getting too big, lets remove all movies that were released before 2005.**_

> DELETE FROM Movies WHERE Year < 2005;
---
_**2. Andrew Stanton has also left the studio, so please remove all movies directed by him.**_

> DELETE FROM Movies WHERE Director = 'Andrew Stanton';

# SQL Lesson 16: Creating tables

---

>_In this exercise, you'll need to create a new table for us to insert some new rows into._

---

### Exercise 16 — Tasks

_**1. Create a new table named Database with the following columns: – Name A string (text) describing the name of the database – Version A number (floating point) of the latest version of this database – Download_count An integer count of the number of times this database was downloaded. This table has no constraints.**_

> CREATE TABLE Database  
> (Name TEXT,  
> Version REAL,  
> Download_count INTEGER);

# SQL Lesson 17: Altering tables

---

>_Our exercises use an implementation that only support adding new columns, so give that a try below._

---

### Exercise 17 — Tasks

_**1. Add a column named Aspect_ratio with a FLOAT data type to store the aspect-ratio each movie was released in.**_

> ALTER TABLE Movies  
> ADD Aspect_ratio FLOAT;
 ---

_**2. Add another column named Language with a TEXT data type to store the language that the movie was released in. Ensure that the default for this language is English.**_

> ALTER TABLE Movies  
> ADD COLUMN Language TEXT DEFAULT 'English';

# SQL Lesson 18: Dropping tables

---

>_We've reached the end of our exercises, so lets clean up by removing all the tables we've worked with._

---

### Exercise 18 — Tasks

_**1. We've sadly reached the end of our lessons, lets clean up by removing the Movies table.**_

> DROP TABLE IF EXISTS Movies;
---
_**2. And drop the BoxOffice table as well.**_

> DROP TABLE IF EXISTS BoxOffice;


---

🎉 **Congratulations!**  
You've completed all SQL lessons and successfully practiced how to query, modify, and manage data in a database.

> Keep exploring, keep learning — the more you practice SQL, the more natural it becomes.

🧠 _Happy querying!_
