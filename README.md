# DataCamp-Exercises
Exercises from the SQL Fundamentals Track by DataCamp

## Table of Contents


## Introduction To SQL
### Querying
#### Querying the books table
1. Use SQL to rreturn a result set of all book titles included in the books table.
```
SELECT title
FROM books;
```

2. Select bith the title and author fields from books.
```
SELECT title, author
FROM books;
```

4. Select all fields from the books table.
```
SELECT *
FROM books;
```

#### Making queries DISTINCT
1. Write SQL code that returns a result set with just one column listing the unique authors in the books table.
```
SELECT DISTINCT author 
FROM books;
```
2. Update the code to return the unique author and genre combinations in the books table.
```
SELECT DISTINCT author, genre
FROM books;
```

#### Aliasing
1. Add an alias to the SQL query to rename the author column to unique_author in the result set.
```
SELECT DISTINCT author AS unique_author 
FROM books;
```

#### VIEWing your query
1. Add a single line of code that saves the results of the written query as a view called library_authors.
```
CREATE VIEW library_authors AS
SELECT DISTINCT author AS unique_author
FROM books;
```
2. Check that the view was created by selecting all columns from library_authors.
```
SELECT * 
FROM library_authors;
```

#### Limiting results
1. Using PostgreSQL, select the genre field from the books table; limit the number of results to 10.
```
SELECT genre
FROM books
LIMIT 10;
```


## Intermediate SQL

### Selecting Data

#### Practice with COUNT()
1. Count the total number of records in the people table, aliasing the result as count_records.
```
SELECT COUNT(people) AS count_records
FROM people;
```
2. Count the number of records with a birthdate in the people table, aliasing the result as count_birthdate.
```
SELECT COUNT(birthdate) AS count_birthdate
FROM people;
```
3. Count the records for languages and countries in the films table; alias as count_languages and count_countries.
```
SELECT COUNT(language) AS count_languages, COUNT(country) AS count_countries
FROM films;
```

#### SELECT DISTINCT
1. Return the unique countries represented in the films table using DISTINCT.
```
SELECT DISTINCT country 
FROM films;
```
2. Return the number of unique countries represented in the films table, aliased as count_distinct_countries.
```
SELECT COUNT(DISTINCT country) AS count_distinct_countries
FROM films;
```
### Filtering Records

#### Using WHERE with numbers
1. Select the film_id and imdb_score from the reviews table and filter on scores higher than 7.0.
```
SELECT film_id, imdb_score
FROM reviews
WHERE imdb_score > 7.0;
```
2. Select the film_id and facebook_likes of the first ten records with less than 1000 likes from the reviews table.
```
SELECT film_id, facebook_likes
FROM reviews
WHERE facebook_likes < 1000
LIMIT 10;
```
3. Count how many records have a num_votes of at least 100,000; use the alias films_over_100K_votes.
```
SELECT COUNt(num_votes) AS films_over_100K_votes
FROM reviews
WHERE num_votes >= 100000;
```

#### Using WHERE with text
1. Select and count the language field using the alias count_spanish. Apply a filter to select only Spanish from the language field.
```
SELECT COUNT(language) AS count_spanish
FROM films
WHERE language = 'Spanish';
```

#### Using AND
1. Select the title and release_year for all German-language films released before 2000.
```
SELECT title, release_year
FROM films
WHERE language = 'German' AND release_year < 2000;
```
2. Update the query from the previous step to show German-language films released after 2000 rather than before.
```
SELECT title, release_year
FROM films
WHERE release_year > 2000
	AND language = 'German';
```
3. Select all details for German-language films released after 2000 but before 2010 using only WHERE and AND.
```
SELECT * 
FROM films
WHERE language = 'German' AND release_year > 2000 AND release_year < 2010;
```

#### Using OR
1. Select the title and release_year for films released in 1990 or 1999 using only WHERE and OR.
```
SELECT title, release_year
FROM films
WHERE release_year = 1990 OR release_year = 1999;
```
#### Using BETWEEN
1. Select the title and release_year of all films released between 1990 and 2000 (inclusive) using BETWEEN.
```
SELECT title, release_year 
FROM films
WHERE release_year BETWEEN 1990 AND 2000;
```
2. Build on your previous query to select only films with a budget over $100 million.
```
SELECT title, release_year
FROM films
WHERE release_year BETWEEN 1990 AND 2000
	AND budget > 100000000;
```
3. Now, restrict the query to only return Spanish-language films.
```
SELECT title, release_year
FROM films
WHERE release_year BETWEEN 1990 AND 2000
	AND budget > 100000000
	AND language = 'Spanish';
```
4. Finally, amend the query to include all Spanish-language or French-language films with the same criteria.
```
SELECT title, release_year
FROM films
WHERE release_year BETWEEN 1990 AND 2000
	AND budget > 100000000
	AND (language = 'Spanish' OR language = 'French');
```

#### LIKE and NOT LIKE
1. Select the names of all people whose names begin with 'B'.
```
SELECT name
FROM people
WHERE name LIKE 'B%';
```
2. Select the names of people whose names have 'r' as the second letter.
```
SELECT name
FROM people
WHERE name LIKE '_r%';
```
3. Select the names of people whose names don't start with 'A'.
```
SELECT name
FROM people
WHERE name NOT LIKE 'A%';
```
#### WHERE IN
1. Select the title and release_year of all films released in 1990 or 2000 that were longer than two hours.
```
SELECT title, release_year
FROM films
WHERE duration > 120 
AND release_year IN(1990,2000);
```
2. Select the title and language of all films in English, Spanish, or French using IN.
```
SELECT title, language
FROM films
WHERE language IN ('English', 'Spanish', 'French')
```
3. Select the title, certification and language of all films certified NC-17 or R that are in English, Italian, or Greek.
```
SELECT title, certification, language
FROM films
WHERE certification IN ('NC-17','R') AND language IN ('English', 'Italian', 'Greek');
```

#### Combining filtering and selecting
1. Count the unique titles from the films database and use the alias provided. Filter to include only movies with a release_year from 1990 to 1999, inclusive. Add another filter narrowing your query down to English-language films. Add a final filter to select only films with 'G', 'PG', 'PG-13' certifications.
```
SELECT COUNT(DISTINCT title) AS nineties_english_films_for_teens
FROM films
WHERE release_year BETWEEN 1990 AND 1999
AND language = 'English'
AND certification IN ('G','PG','PG-13');
```

#### Practice with NULLs
1. Select the title of every film that doesn't have a budget associated with it and use the alias no_budget_info.
```
SELECT title AS no_budget_info
FROM films
WHERE budget IS NULL;
```
2. Count the number of films with a language associated with them and use the alias count_language_known.
```
SELECT COUNT(language) AS count_language_known
FROM films;
```
### Aggregate Functions

#### Practive with aggregate functions
1. Use the SUM() function to calculate the total duration of all films and alias with total_duration.
```
SELECT SUM(duration) AS total_duration
FROM films;
```
2. Calculate the average duration of all films and alias with average_duration.
```
SELECT AVG(duration) AS average_duration
FROM films;
```
3. Find the most recent release_year in the films table, aliasing as latest_year.
```
SELECT MAX(release_year) AS latest_year
FROM films;
```
4. Find the duration of the shortest film and use the alias shortest_film.
```
SELECT MIN(duration) AS shortest_film
FROM films;
```

#### Combining aggregate functions with WHERE
1. Use SUM() to calculate the total gross for all films made in the year 2000 or later, and use the alias total_gross.
```
SELECT SUM(gross) AS total_gross
FROM films
WHERE release_year >= 2000;
```
2. Calculate the average amount grossed by all films whose titles start with the letter 'A' and alias with avg_gross_A.
```
SELECT AVG(gross) AS avg_gross_A
FROM films
WHERE title LIKE 'A%';
```
3. Calculate the lowest gross film in 1994 and use the alias lowest_gross.
```
SELECT MIN(gross) AS lowest_gross
FROM films
WHERE release_year = 1994;
```
4. Calculate the highest gross film between 2000 and 2012, inclusive, and use the alias highest_gross.
```
SELECT MAX(gross) AS highest_gross
FROM films
WHERE release_year BETWEEN 2000 AND 2012;
```

#### Using ROUND()
1. Calculate the average facebook_likes to one decimal place and assign to the alias, avg_facebook_likes.
```
SELECT ROUND(AVG(facebook_likes),1) AS avg_facebook_likes
FROM reviews
```

#### ROUND() with a negative parameter
1. Calculate the average budget from the films table, aliased as avg_budget_thousands, and round to the nearest thousand.
```
SELECT ROUND(AVG(budget),-3) AS avg_budget_thousands
FROM films;
```

#### Aliasing with functions
1. Select the title and duration in hours for all films and alias as duration_hours; since the current durations are in minutes, you'll need to divide duration by 60.0.
```
SELECT title, duration/60.0 AS duration_hours
FROM films;
```
2. Calculate the percentage of people who are no longer alive and alias the result as percentage_dead.
```
SELECT COUNT(deathdate) * 100.0 / COUNT(name) AS percentage_dead
FROM people;
```
3. Find how many decades (period of ten years) the films table covers by using MIN() and MAX(); alias as number_of_decades.
```
SELECT (MAX(release_year) - MIN(release_year)) / 10.0 AS number_of_decades
FROM films;
```

#### Rounding results
1. Update the query by adding ROUND() around the calculation and round to two decimal places.
```
SELECT title, ROUND(duration / 60.0,2) AS duration_hours
FROM films;
```

### Sorting and Grouping

#### Sorting single fields
1. Select the name of each person in the people table, sorted alphabetically.
```
SELECT name 
FROM people
```
2. Select the title and duration for every film, from longest duration to shortest.
```
SELECT title, duration 
FROM films
ORDER BY duration DESC;
```
#### Sorting multiple fields
1. Select the release_year, duration, and title of films ordered by their release year and duration, in that order.
```
SELECT release_year, duration, title
FROM films
ORDER BY release_year, duration;
```
2. Select the certification, release_year, and title from films ordered first by certification (alphabetically) and second by release year, starting with the most recent year.
```
SELECT certification, release_year, title
FROM films
ORDER BY certification, release_year DESC;
```
#### GROUP BY single fields
1. Select the release_year and count of films released in each year aliased as film_count.
```
SELECT release_year, COUNT(*) AS film_count
FROM films
GROUP BY release_year;
```
2. Select the release_year and average duration aliased as avg_duration of all films, grouped by release_year.
```
SELECT release_year, AVG(duration) AS avg_duration
FROM films
GROUP BY release_year;
```

#### GROUP BY multiple fields
1. Select the release_year, country, and the maximum budget aliased as max_budget for each year and each country; sort your results by release_year and country.
```
SELECT release_year, country, MAX(budget) AS max_budget
FROM films
GROUP BY release_year, country;
```

#### Filtering with HAVING

#### HAVING and sorting
1. Select the country and the average budget as average_budget, rounded to two decimal, from films. Group the results by country. Filter the results to countries with an average budget of more than one billion (1000000000). Sort by descending order of the average_budget.
```
SELECT country, AVG(budget) AS average_budget
FROM films
GROUP BY country
HAVING AVG(budget) > 1000000000
ORDER BY average_budget
```

#### All together now
1. Select the release_year for each film in the films table, filter for records released after 1990, and group by release_year.
```
SELECT release_year 
FROM films
GROUP BY release_year
HAVING release_year > 1990;
```
2. Modify the query to include the average budget aliased as avg_budget and average gross aliased as avg_gross for the results we have so far.
```
SELECT release_year, AVG(budget) AS avg_budget, AVG(gross) AS avg_gross
FROM films
WHERE release_year > 1990
GROUP BY release_year;
```
3. Modify the query once more so that only years with an average budget of greater than 60 million are included.
```
SELECT release_year, AVG(budget) AS avg_budget, AVG(gross) AS avg_gross
FROM films
WHERE release_year > 1990
GROUP BY release_year
HAVING AVG(budget) > 60000000;
```
4. Finally, order the results from the highest average gross and limit to one.
```
SELECT release_year, AVG(budget) AS avg_budget, AVG(gross) AS avg_gross
FROM films
WHERE release_year > 1990
GROUP BY release_year
HAVING AVG(budget) > 60000000
ORDER BY avg_gross DESC
LIMIT 1;
```

## Joining Data in SQL

### Introducing Inner Joins

#### Your first join
1. Perform an inner join with the cities table on the left and the countries table on the right; do not alias tables here or in the next step. Identify the relevant column names to join ON by inspecting the cities and countries tabs in the console.
```
SELECT * 
FROM cities
INNER JOIN countries
ON cities.country_code = countries.code;
```
2. Complete the SELECT statement to keep only the name of the city, the name of the country, and the region the country is located in (in the order specified). Alias the name of the city AS city and the name of the country AS country.
```
SELECT cities.name AS city, countries.name AS country, region
FROM cities
INNER JOIN countries
ON cities.country_code = countries.code;
```
#### Joining with aliased tables
1. Start with your inner join in line 5; join the tables countries AS c (left) with economies (right), aliasing economies AS e. Next, use code as your joining field in line 7; do not use the USING command here.
Lastly, select the following columns in order in line 2: code from the countries table (aliased as country_code), name, year, and inflation_rate.
```
SELECT c.code AS country_code, name, year, inflation_rate
FROM countries AS c
INNER JOIN economies AS e
ON c.code = e.code;
```
#### USING in action
1. Use the country code field to complete the INNER JOIN with USING; do not change any alias names.
```
SELECT c.name AS country, l.name AS language, official
FROM countries AS c
INNER JOIN languages AS l
USING (code);
```
#### Inspecting a relationship
1. Start with the join statement in line 6; perform an inner join with the countries table as c on the left with the languages table as l on the right. Make use of the USING keyword to join on code in line 8. Lastly, in line 2, select the country name, aliased as country, and the language name, aliased as language.
```
SELECT c.name AS country, l.name AS language  
FROM countries AS c
INNER JOIN languages AS l
USING (code);
```
2. Rearrange the SELECT statement so that the language column appears on the left and the country column on the right. Sort the results by language.
```
SELECT l.name AS language, c.name AS country
FROM countries AS c
INNER JOIN languages AS l
USING(code)
ORDER BY language;
```
#### Joining multiple tables
1. Perform an inner join of countries AS c (left) with populations AS p (right), on code.
Select name, year and fertility_rate.
```
 SELECT name, year, fertility_rate
FROM countries AS c
INNER JOIN populations AS p
ON c.code = p.country_code;
```
2. Chain another inner join to your query with the economies table AS e, using code.
Select name, and using table aliases, select year and unemployment_rate from economies.
```
SELECT name, e.year, fertility_rate, e.unemployment_rate
FROM countries AS c
INNER JOIN populations AS p
ON c.code = p.country_code
INNER JOIN economies AS e
ON c.code = e.code;
```
#### Checking multi-table joins
1. Modify your query so that you are joining to economies on year as well as code.
```
SELECT name, e.year, fertility_rate, unemployment_rate
FROM countries AS c
INNER JOIN populations AS p
ON c.code = p.country_code
INNER JOIN economies AS e
ON c.code = e.code AND p.year = e.year;
```

### Outer Joins, Cross Joins and Self Joins

#### This is a LEFT JOIN, right?
1. Perform an inner join with cities AS c1 on the left and countries as c2 on the right.
Use code as the field to merge your tables on.
```
SELECT 
    c1.name AS city,
    code,
    c2.name AS country,
    region,
    city_proper_pop
FROM cities AS c1
INNER JOIN countries AS c2
ON c1.country_code = c2.code
ORDER BY code DESC;
```
2. Change the code to perform a LEFT JOIN instead of an INNER JOIN.
After executing this query, have a look at how many records the query result contains.
```
SELECT 
	c1.name AS city, 
    code, 
    c2.name AS country,
    region, 
    city_proper_pop
FROM cities AS c1
LEFt JOIN countries AS c2
ON c1.country_code = c2.code
ORDER BY code DESC;
```

#### Building on your LEFT JOIN
1. Complete the LEFT JOIN with the countries table on the left and the economies table on the right on the code field. Filter the records from the year 2010.
```
SELECT name, region, gdp_percapita
FROM countries AS c
LEFT JOIN economies AS e
ON c.code = e.code
WHERE year = 2010;
```
2. To calculate per capita GDP per region, begin by grouping by region.
After your GROUP BY, choose region in your SELECT statement, followed by average GDP per capita using the AVG() function, with AS avg_gdp as your alias.
```
SELECT region, AVG(gdp_percapita) AS avg_gdp
FROM countries AS c
LEFT JOIN economies AS e
USING(code)
WHERE year = 2010
GROUP BY region;
```
3. Order the result set by the average GDP per capita from highest to lowest.
Return only the first 10 records in your result.
```
SELECT region, AVG(gdp_percapita) AS avg_gdp
FROM countries AS c
LEFT JOIN economies AS e
USING(code)
WHERE year = 2010
GROUP BY region
ORDER BY avg_gdp DESC
LIMIT 10;
```

#### Is this RIGHT?
1. Write a new query using RIGHT JOIN that produces an identical result to the LEFT JOIN provided.
```
SELECT countries.name AS country, languages.name AS language, percent
FROM languages
RIGHT JOIN countries
USING(code)
ORDER BY language;
```

#### Comparing joins
1. Perform a full join with countries (left) and currencies (right). Filter for the North America region or NULL country names.
```
SELECT name AS country, code, region, basic_unit
FROM countries
FULL JOIN currencies 
USING (code)
WHERE region = 'North America' OR name IS null
ORDER BY region;
```
2. Repeat the same query as before, turning your full join into a left join with the currencies table. Have a look at what has changed in the output by comparing it to the full join result.
```
SELECT name AS country, code, region, basic_unit
FROM countries
LEFT JOIN currencies 
USING (code)
WHERE region = 'North America' 
	OR name IS NULL
ORDER BY region;
```
3. Repeat the same query again, this time performing an inner join of countries with currencies. Have a look at what has changed in the output by comparing it to the full join and left join results!
```
SELECT name AS country, code, region, basic_unit
FROM countries
-- Join to currencies
INNER JOIN currencies 
USING (code)
WHERE region = 'North America' 
	OR name IS NULL
ORDER BY region;
```
#### Chaining FULL JOINs
1. Complete the FULL JOIN with countries as c1 on the left and languages as l on the right, using code to perform this join. Next, chain this join with another FULL JOIN, placing currencies on the right, joining on code again.
```
SELECT 
	c1.name AS country, 
    region, 
    l.name AS language,
	basic_unit, 
    frac_unit
FROM countries as c1 
FULL JOIN languages AS l
USING (code)
FULL JOIN currencies AS c2
USING (code)
WHERE region LIKE 'M%esia';
```

#### Histories and Languages
1. Complete the code to perform an INNER JOIN of countries AS c with languages AS l using the code field to obtain the languages currently spoken in the two countries.
```
SELECT c.name AS country, l.name AS language
FROM countries AS c
INNER JOIN languages AS l
ON c.code = l.code
WHERE c.code IN ('PAK','IND')
	AND l.code in ('PAK','IND');
```
2. Change your INNER JOIN to a different kind of join to look at possible combinations of languages that could have been spoken in the two countries given their history. Observe the differences in output for both joins.
```
SELECT c.name AS country, l.name AS language
FROM countries AS c        
CROSS JOIN languages AS l
WHERE c.code in ('PAK','IND')
	AND l.code in ('PAK','IND');
```

#### Choosing your join
1. Complete the join of countries AS c with populations as p. Filter on the year 2010.
Sort your results by life expectancy in ascending order. Limit the result to five countries.
```
SELECT 
	c.name AS country,
    region,
    life_expectancy AS life_exp
FROM countries AS c
LEFT JOIN populations AS p 
ON c.code = p.country_code
Where year = 2010
ORDER BY life_exp 
LIMIT 5;
```

#### Comparing a country to itself
1. Perform an inner join of populations with itself ON country_code, aliased p1 and p2 respectively. Select the country_code from p1 and the size field from both p1 and p2, aliasing p1.size as size2010 and p2.size as size2015 (in that order).
```
SELECT p1.country_code, p1.size AS size2010, p2.size AS size2015
FROM populations AS p1
INNER JOIN populations AS p2
ON p1.country_code = p2.country_code;
```
2.  Since you want to compare records from 2010 and 2015, eliminate unwanted records by extending the WHERE statement to include only records where the p1.year matches p2.year - 5.
```
SELECT 
	p1.country_code, 
    p1.size AS size2010, 
    p2.size AS size2015
FROM populations AS p1
INNER JOIN populations AS p2
ON p1.country_code = p2.country_code
WHERE p1.year = 2010
    AND p1.year = p2.year - 5;
```

### Set Theory for SQL Joins

#### Comparing global economies
1. Begin your query by selecting all fields from economies2015. Create a second query that selects all fields from economies2019. Perform a set operation to combine the two queries you just created, ensuring you do not return duplicates.
```
SELECT *
FROM economies2015
UNION
SELECT *
FROM economies2019
ORDER BY code, year;
```
#### Comparing two set operations
1. Perform an appropriate set operation that determines all pairs of country code and year (in that order) from economies and populations, excluding duplicates. Order by country code and year.
```
SELECT code, year
FROM economies
UNION
SELECT country_code AS code, year
FROM populations;
```
2. Amend the query to return all combinations (including duplicates) of country code and year in the economies or the populations tables.
```
SELECT code, year
FROM economies
-- Set theory clause
UNION ALL
SELECT country_code, year
FROM populations
ORDER BY code, year;
```

#### INTERSECT
1. Return all city names that are also country names.
```
SELECT name
FROM cities
INTERSECT
SELECT name
FROM countries;
```
#### You've got it, EXCEPT
1. Return all cities that do not have the same name as a country.
```
SELECT name
FROM cities
EXCEPT 
SELECT name
FROM countries
ORDER BY name;
```

### Subqueries

#### Semi join
1. Select country code as a single field from the countries table, filtering for countries in the 'Middle East' region.
```
SELECT code
FROM countries
WHERE region = 'Middle East';
```
2. Write a second query to SELECT the name of each unique language appearing in the languages table; do not use column aliases here. Order the result set by name in ascending order.
```
SELECT DISTINCT name
FROM languages
ORDER BY name;
```
3. Create a semi join out of the two queries you've written, which filters unique languages returned in the first query for only those languages spoken in the 'Middle East'.
```
SELECT DISTINCT name
FROM languages
WHERE code IN
    (SELECT code
    FROM countries
    WHERE region = 'Middle East')
ORDER BY name;
```

#### Disgnosing problems using anti join
1. Begin by writing a query to return the code and name (in order, not aliased) for all countries in the continent of Oceania from the countries table. Observe the number of records returned and compare this with the provided INNER JOIN, which returns 15 records.
```
SELECT code, name
FROM countries
WHERE continent = 'Oceania'
```
2. Now, build on your query to complete your anti join, by adding an additional filter to return every country code that is not included in the currencies table.
```
SELECT code, name
FROM countries
WHERE continent = 'Oceania'
  AND code NOT IN 
    (SELECT code
    FROM currencies);
```

#### Subquery inside WHERE
1. Begin by calculating the average life expectancy from the populations table. Filter your answer to use records from 2015 only.
```
SELECT AVG(life_expectancy)
FROM populations
WHERE year = 2015;
```
2. The answer from your query has now been nested into another query; use this calculation to filter populations for all records where life_expectancy is 1.15 times higher than average.
```
SELECT *
FROM populations
WHERE life_expectancy > 1.15 * 
  (SELECT AVG(life_expectancy) 
   FROM populations
   WHERE year = 2015) 
    AND year = 2015;
```

#### WHERE do people love?
1. Return the name, country_code and urbanarea_pop for all capital cities (not aliased).
```
SELECT name, country_code, urbanarea_pop
FROM cities
WHERE name IN    
    (SELECT capital
    FROM countries)
ORDER BY urbanarea_pop DESC;
```

#### Subquery inside SELECT
1. Write a LEFT JOIN with countries on the left and the cities on the right, joining on country code. In the SELECT statement of your join, include country names as country, and count the cities in each country, aliased as cities_num. Sort by cities_num (descending), and country (ascending), limiting to the first nine records.
```
SELECT countries.name AS country, COUNT(*) AS cities_num
FROM countries
LEFT JOIN cities
ON countries.code = cities.country_code
GROUP BY country
ORDER BY cities_num DESC, country
LIMIT 9;
```
2. Complete the subquery to return a result equivalent to your LEFT JOIN, counting all cities in the cities table as cities_num. Use the WHERE clause to enable the correct country codes to be matched in the cities and countries columns.
```
SELECT countries.name AS country,
  (SELECT COUNT(*)
   FROM cities
   WHERE cities.country_code = countries.code) AS cities_num
FROM countries
ORDER BY cities_num DESC, country
LIMIT 9;
```

#### Subquery inside FROM
1. Begin with a query that groups by each country code from languages, and counts the languages spoken in each country as lang_num. In your SELECT statement, return code and lang_num (in that order).
```
SELECT code, COUNT(*) AS lang_num
FROM languages
GROUP BY code;
```
2. Select local_name from countries, with the aliased lang_num from your subquery (which has been nested and aliased for you as sub). Use WHERE to match the code field from countries and sub.
```
SELECT countries.local_name, sub.lang_num
FROM countries,
  (SELECT code, COUNT(*) AS lang_num
  FROM languages
  GROUP BY code) AS sub
WHERE countries.code = sub.code
ORDER BY lang_num DESC;
```

#### Subquery challenge
1. Select country code, inflation_rate, and unemployment_rate from economies.
Filter code for the set of countries which do not contain the words "Republic" or "Monarchy" in their gov_form.
```
SELECT code, inflation_rate, unemployment_rate
FROM economies
WHERE year = 2015 
  AND code NOT IN
	(SELECT code
  FROM countries 
  WHERE gov_form LIKE '%Republic%' OR gov_form LIKE '%Monarchy%')
ORDER BY inflation_rate;
```

#### Final challenge 

## Data Manipulation in SQL

## PostgreSQL Summary Stats and Window Function
