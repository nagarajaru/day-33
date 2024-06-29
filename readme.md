# DAY 33 TASK

* EXERCISE 1   ![alt text](<Screenshot 2024-06-29 071253-1.jpg>)

SELECT title 
FROM movies;


SELECT director
FROM movies;


SELECT title, director
FROM movies;


SELECT title, year
FROM movies;


SELECT *
FROM movies;

* EXERCISE 2   ![alt text](<Screenshot 2024-06-29 071457.jpg>)

SELECT * 
FROM movies
WHERE id = 6;


SELECT *
FROM movies 
WHERE year BETWEEN 2000 and 2010;


SELECT *
FROM movies
WHERE year NOT BETWEEN 2000 and 2010;


SELECT *
FROM movies
WHERE id BETWEEN 1 AND 5;

* EXERCISE 3   ![alt text](<Screenshot 2024-06-29 071633-1.jpg>)

SELECT *
FROM movies
WHERE title LIKE "%Toy Story%";


SELECT *
FROM movies
WHERE director = "John Lasseter";


SELECT *
FROM movies
WHERE director != "John Lasseter";


SELECT *
FROM movies
WHERE title LIKE "WALL-%";

* EXERCISE 4   ![alt text](<Screenshot 2024-06-29 071812.jpg>)

SELECT DISTINCT director 
FROM movies
ORDER BY director ASC;


SELECT *
FROM movies
ORDER BY year DESC
LIMIT 4;


SELECT *
FROM movies
ORDER BY title ASC
LIMIT 5;


SELECT *
FROM movies
ORDER BY title ASC
LIMIT 5
OFFSET 5;

* EXERCISE 5   ![alt text](<Screenshot 2024-06-29 072051.jpg>)

SELECT country, population 
FROM north_american_cities
WHERE country = "Canada";


SELECT city
FROM north_american_cities
WHERE country = "United States"
ORDER BY latitude DESC;


SELECT city
FROM north_american_cities
WHERE longitude < (
	SELECT longitude
	FROM north_american_cities
	WHERE city = "Chicago"
)
ORDER BY longitude ASC;


SELECT city
FROM north_american_cities
WHERE country = "Mexico" 
ORDER BY population DESC
LIMIT 2;


SELECT city, population
FROM north_american_cities
WHERE country = "United States"
ORDER BY population DESC
LIMIT 2
OFFSET 2;

* EXERCISE 6   ![alt text](<Screenshot 2024-06-29 072213.jpg>)

SELECT title, domestic_sales, international_sales
FROM movies
INNER JOIN boxoffice
	ON movies.id = boxoffice.movie_id;


SELECT *
FROM movies
INNER JOIN boxoffice
	ON movies.id = boxoffice.movie_id
WHERE international_sales > domestic_sales;


SELECT title, rating
FROM movies
INNER JOIN boxoffice
	ON movies.id = boxoffice.movie_id
ORDER BY rating DESC;

* EXERCISE 7   ![alt text](<Screenshot 2024-06-29 072340.jpg>)

SELECT DISTINCT building_name
FROM buildings
LEFT JOIN employees
	ON buildings.building_name = employees.building
WHERE building IS NOT NULL;


SELECT *
FROM buildings;


SELECT DISTINCT building_name, role
FROM buildings
LEFT JOIN employees
	ON buildings.building_name = employees.building;

* EXERCISE 8   ![alt text](<Screenshot 2024-06-29 072438.jpg>)

SELECT *
FROM employees
LEFT JOIN buildings
	ON employees.building = buildings.building_name
WHERE building_name IS NULL;


SELECT *
FROM buildings
LEFT JOIN employees
	ON buildings.building_name = employees.building
WHERE role IS NULL;

* EXERCISE 9   ![alt text](<Screenshot 2024-06-29 072609.jpg>)

SELECT
	title,
	(domestic_sales + international_sales)/1000000 AS sales
FROM boxoffice AS b
INNER JOIN movies AS m
	ON m.id = b.movie_id;


SELECT
	title,
	rating*10 AS ratings_percent
FROM boxoffice AS b
INNER JOIN movies AS m
	ON m.id = b.movie_id;


SELECT title, year
FROM boxoffice AS b
INNER JOIN movies AS m
	ON m.id = b.movie_id
WHERE year % 2 = 0
ORDER BY year ASC;

* EXERCISE 10  ![alt text](<Screenshot 2024-06-29 072726.jpg>)

SELECT MAX(years_employed) as longest_years
FROM employees;


SELECT
    role,
    AVG(years_employed)AS average_years_employed
FROM employees
GROUP BY role;


SELECT
    building,
    SUM(years_employed)AS sum_of_years_employed
FROM employees
GROUP BY building;

* EXERCISE 11  ![alt text](<Screenshot 2024-06-29 072837.jpg>)

SELECT COUNT(role)
FROM employees
WHERE role = 'Artist';

SELECT
    role,
    COUNT(name) AS number_of_employees
FROM employees
GROUP BY role;

SELECT
	role,
	SUM(years_employed)
FROM employees
GROUP BY role
HAVING role = "Engineer";

* EXERCISE 12  ![alt text](<Screenshot 2024-06-29 073007.jpg>)

SELECT
	director,
	COUNT(*)
FROM movies
GROUP BY director;


SELECT
    director,
    SUM(domestic_sales + international_sales) AS total_sales 
FROM movies
INNER JOIN boxoffice
    ON movies.id = boxoffice.movie_id
GROUP BY director;

* EXERCISE 13  ![alt text](<Screenshot 2024-06-29 073118.jpg>)

INSERT INTO movies
    (title, director, year, length_minutes)
VALUES
    ('Toy Story 4', 'Lance Lafontaine', 2984, 15);


INSERT INTO boxoffice
    (movie_id, rating, domestic_sales, international_sales)
VALUES
    (15, 8.7, 340000000, 270000000);

* EXERCISE 14  ![alt text](<Screenshot 2024-06-29 073320.jpg>)

UPDATE movies
SET director = "John Lasseter"
WHERE title = "A Bug's Life";


UPDATE movies
SET
    title = 'Toy Story 3',
    director = 'Lee Unkrich'
WHERE id = (
    SELECT id
    FROM movies
    WHERE title = 'Toy Story 8'
); 

* EXERCISE 15  ![alt text](<Screenshot 2024-06-29 073424.jpg>)

DELETE FROM movies
WHERE year < 2005;


DELETE FROM movies
WHERE director = 'Andrew Stanton';

* EXERCISE 16  ![alt text](<Screenshot 2024-06-29 073525.jpg>)

CREATE TABLE IF NOT EXISTS Database (
    Name TEXT,
    Version FLOAT,
    Download_count INTEGER
);

* EXERCISE 17  ![alt text](<Screenshot 2024-06-29 073625.jpg>)

ALTER TABLE movies
ADD aspect_ratio FLOAT;


ALTER TABLE movies
ADD language TEXT
    DEFAULT 'English';

* EXERCISE 18  ![alt text](<Screenshot 2024-06-29 073744.jpg>)

DROP TABLE IF EXISTS mytable;


DROP TABLE IF EXISTS boxoffice;