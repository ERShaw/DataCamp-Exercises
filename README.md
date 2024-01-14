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

#### Building on Subqueries in FROM
1. Complete the subquery inside the FROM clause. Select the country name from the country table, along with the date, the home goal, the away goal, and the total goals columns from the match table. Create a column in the subquery that adds home and away goals, called total_goals. This will be used to filter the main query. Select the country, date, home goals, and away goals in the main query. Filter the main query for games with 10 or more total goals.
```
SELECT
    country,
    date,
    home_goal,
    away_goal
FROM
subquery
	(SELECT c.name AS country, 
     	    m.date, 
     		m.home_goal, 
     		m.away_goal,
           (m.home_goal + m.away_goal) AS total_goals
    FROM match AS m
    LEFT JOIN country AS c
    ON m.country_id = c.id) AS subquery
WHERE total_goals >= 10;
```
#### Add a subquery to the SELECT clause
1. In the subquery, select the average total goals by adding home_goal and away_goal.
Filter the results so that only the average of goals in the 2013/2014 season is calculated. In the main query, select the average total goals by adding home_goal and away_goal. This calculates the average goals for each league. Filter the results in the main query the same way you filtered the subquery. Group the query by the league name.
```
SELECT 
	l.name AS league,
    ROUND(AVG(m.home_goal + m.away_goal), 2) AS avg_goals,
    (SELECT ROUND(AVG(home_goal + away_goal), 2) 
     FROM match
     WHERE season = '2013/2014') AS overall_avg
FROM league AS l
LEFT JOIN match AS m
ON l.country_id = m.country_id
WHERE season = '2013/2014'
GROUP BY name;
```
#### Subqueries in Select for Calculations
1. Select the average goals scored in a match for each league in the main query.
Select the average goals scored in a match overall for the 2013/2014 season in the subquery. Subtract the subquery from the average number of goals calculated for each league. Filter the main query so that only games from the 2013/2014 season are included.
```
SELECT l.name AS league,
	ROUND(AVG(m.home_goal + m.away_goal),2) AS avg_goals,
	ROUND(AVG(m.home_goal + m.away_goal) - (SELECT AVG(home_goal + away_goal)
	FROM match WHERE season = '2013/2014'),2) AS diff
FROM league AS l
LEFT JOIN match AS m
ON l.country_id = m.country_id
WHERE m.season = '2013/2014'
GROUP BY l.name;
```

#### ALL the subqueries EVERYWHERE
1. Extract the average number of home and away team goals in two SELECT subqueries.
Calculate the average home and away goals for the specific stage in the main query. Filter both subqueries and the main query so that only data from the 2012/2013 season is included. Group the query by the m.stage column.
```
SELECT m.stage,
    ROUND(AVG(m.home_goal + m.away_goal),2) AS avg_goals,
    ROUND((SELECT AVG(home_goal + away_goal) 
    FROM match WHERE season = '2012/2013'),2) AS overall
FROM match AS m
WHERE season = '2012/2013'
GROUP BY m.stage;
```
#### Add a subquery in FROM
1. Calculate the average home goals and average away goals from the match table for each stage in the FROM clause subquery. Add a subquery to the WHERE clause that calculates the overall average home goals. Filter the main query for stages where the average home goals is higher than the overall average. Select the stage and avg_goals columns from the s subquery into the main query.
```
SELECT s.stage,
    ROUND(s.avg_goals,2) AS avg_goals
FROM (SELECT stage, AVG(home_goal + away_goal) AS avg_goals
     FROM match
     WHERE season = '2012/2013'
     GROUP BY stage) AS s
WHERE s.avg_goals > (SELECT AVG(home_goal + away_goal) 
FROM match WHERE season = '2012/2013');
```
#### Add a subquery in SELECT
1. Create a subquery in SELECT that yields the average goals scored in the 2012/2013 season. Name the new column overall_avg. Create a subquery in FROM that calculates the average goals scored in each stage during the 2012/2013 season. Filter the main query for stages where the average goals exceeds the overall average in 2012/2013.
```
SELECT s.stage,
	ROUND(s.avg_goals,2) AS avg_goal,
	(SELECT AVG(home_goal + away_goal) FROM match WHERE season = '2012/2013') AS overall_avg
FROM (SELECT stage, AVG(home_goal + away_goal) AS avg_goals
     FROM match
     WHERE season = '2012/2013'
     GROUP BY stage) AS s
WHERE s.avg_goals > (SELECT AVG(home_goal + away_goal) 
FROM match WHERE season = '2012/2013');
```
#### Basic Correlated Subqueries
1. Select the country_id, date, home_goal, and away_goal columns in the main query.
Complete the AVG value in the subquery. Complete the subquery column references, so that country_id is matched in the main and subquery.
```
SELECT m.country_id,
    m.date,
    m.home_goal, 
    m.away_goal
FROM match AS m
WHERE (home_goal + away_goal) > (SELECT AVG((sub.home_goal + sub.away_goal) * 3)
FROM match AS sub
WHERE m.country_id = sub.country_id);
```
#### Correlated subquery with multiple conditions
1. Select the country_id, date, home_goal, and away_goal columns in the main query.
Complete the subquery: Select the matches with the highest number of total goals.
Match the subquery to the main query using country_id and season. Fill in the correct logical operator so that total goals equals the max goals recorded in the subquery.
```
SELECT main.country_id,
    main.date,
    main.home_goal,
    main.away_goal
FROM match AS main
WHERE (home_goal + away_goal) = (SELECT MAX(sub.home_goal + sub.away_goal)
FROM match AS sub
WHERE main.country_id = sub.country_id 
AND main.season = sub.season);
```
#### Nested simple subqueries
1. Complete the main query to select the season and the max total goals in a match for each season. Name this max_goals. Complete the first simple subquery to select the max total goals in a match across all seasons. Name this overall_max_goals. Complete the nested subquery to select the maximum total goals in a match played in July across all seasons. Select the maximum total goals in the outer subquery. Name this entire subquery july_max_goals.
```
SELECT season, MAX(home_goal + away_goal) AS max_goals,
   (SELECT MAX(home_goal + away_goal) FROM match) AS overall_max_goals,
   (SELECT MAX(home_goal + away_goal) 
    FROM match
    WHERE id IN (SELECT id FROM match WHERE EXTRACT(MONTH FROM date) = 07))
	AS july_max_goals
FROM match
GROUP BY season;
```
#### Nest subquery in FROM
1. Generate a list of matches where at least one team scored 5 or more goals.
```
SELECT
	country_id,
    season,
	id
FROM match
WHERE home_goal >= '5' OR away_goal >= '5';
```
2. Turn the query from the previous step into a subquery in the FROM statement. COUNT the match ids generated in the previous step, and group the query by country_id and season.
```
SELECT
    country_id,
    season,
    COUNT(id) AS matches
FROM
	(SELECT
    	country_id,
    	season,
    	id
	FROM match
	WHERE home_goal >= 5 OR away_goal >= 5)
    AS subquery
GROUP BY subquery.country_id, season;
```
3. Finally, declare the same query from step 2 as a subquery in FROM with the alias outer_s. Left join it to the country table using the outer query's country_id column.
Calculate an AVG of high scoring matches per country in the main query.
```
SELECT c.name AS country,
    AVG(outer_s.matches) AS avg_seasonal_high_scores
FROM country AS c
LEFT JOIN (
  SELECT country_id, season,
         COUNT(id) AS matches
  FROM (
    SELECT country_id, season, id
	FROM match
	WHERE home_goal >= 5 OR away_goal >= 5) AS inner_s
  GROUP BY country_id, season) AS outer_s
ON c.id = outer_s.country_id
GROUP BY country;
```
#### Clean up with CTEs
1. Complete the syntax to declare your CTE. Select the country_id and match id from the match table in your CTE. Left join the CTE to the league table using country_id.
```
WITH match_list AS (
    SELECT country_id, id
    FROM match
    WHERE (home_goal + away_goal) >= 10)
SELECT
    l.name AS league,
    COUNT(match_list.id) AS matches
FROM league AS l
LEFT JOIN match_list ON l.id = match_list.country_id
GROUP BY l.name;
```
#### Organizing with CTEs
1. Declare your CTE, where you create a list of all matches with the league name.
Select the league, date, home, and away goals from the CTE. Filter the main query for matches with 10 or more goals.
```
WITH match_list AS (
    SELECT name AS league, 
		m.date, 
  		m.home_goal, 
  		m.away_goal,
       (m.home_goal + m.away_goal) AS total_goals
    FROM match AS m
    LEFT JOIN league as l ON m.country_id = l.id)
SELECT league, date, home_goal, away_goal
FROM match_list
WHERE total_goals >= '10';
```
#### CTEs with nested subqueries
1. Declare a CTE that calculates the total goals from matches in August of the 2013/2014 season. Left join the CTE onto the league table using country_id from the match_list CTE. Filter the list on the inner subquery to only select matches in August of the 2013/2014 season.
```
WITH match_list AS (
    SELECT country_id,
  	   (home_goal + away_goal) AS goals
    FROM match
    WHERE id IN (
       SELECT id
       FROM match
       WHERE season = '2013/2014' AND EXTRACT(MONTH FROM date) = '8'))
SELECT name, AVG(goals)
FROM league AS l
LEFT JOIN match_list ON l.id = match_list.country_id
GROUP BY l.name;
```
#### Get team names with a subquery
1. Create a query that left joins team to match in order to get the identity of the home team. This becomes the subquery in the next step.
```
SELECT m.id, t.team_long_name AS hometeam
FROM match AS m
LEFT JOIN team as t
ON m.hometeam_id = team_api_id;
```
2. Add a second subquery to the FROM statement to get the away team name, changing only the hometeam_id. Left join both subqueries to the match table on the id column.
```
SELECT m.date,
    hometeam,
    awayteam,
    m.home_goal,
    m.away_goal
FROM match AS m
LEFT JOIN (
  SELECT match.id, team.team_long_name AS hometeam
  FROM match
  LEFT JOIN team
  ON match.hometeam_id = team.team_api_id) AS home
ON home.id = m.id
LEFT JOIN (
  SELECT match.id, team.team_long_name AS awayteam
  FROM match
  LEFT JOIN team
  ON match.awayteam_id = team.team_api_id) AS away
ON away.id = m.id;
```
#### Get team names with correlated subqueries
1. Using a correlated subquery in the SELECT statement, match the team_api_id column from team to the hometeam_id from match.
```
SELECT
    m.date,
   (SELECT team_long_name
    FROM team AS t
    WHERE team_api_id = m.hometeam_id) AS hometeam
FROM match AS m;
```
2. Create a second correlated subquery in SELECT, yielding the away team's name.
Select the home and away goal columns from match in the main query.
```
SELECT m.date,
    (SELECT team_long_name
     FROM team AS t
     WHERE t.team_api_id = m.hometeam_id) AS hometeam,
    (SELECT team_long_name
     FROM team AS t
     WHERE team_api_id = m.awayteam_id)
	AS awayteam, home_goal, away_goal
FROM match AS m;
```
#### Get team names with CTEs
1. Select id from match and team_long_name from team. Join these two tables together on hometeam_id in match and team_api_id in team.
```
SELECT m.id, t.team_long_name AS hometeam
FROM match AS m
LEFT JOIN team AS t 
ON team_api_id = hometeam_id;
```
2. Declare the query from the previous step as a common table expression. SELECT everything from the CTE into the main query. Your results will not change at this step!
```
WITH home AS (
	SELECT m.id, t.team_long_name AS hometeam
	FROM match AS m
	LEFT JOIN team AS t 
	ON m.hometeam_id = t.team_api_id)
SELECT *
FROM home;
```
3. Let's declare the second CTE, away. Join it to the first CTE on the id column.
The date, home_goal, and away_goal columns have been added to the CTEs. SELECT them into the main query.
```
WITH home AS (
  SELECT m.id, m.date, t.team_long_name AS hometeam, m.home_goal
  FROM match AS m
  LEFT JOIN team AS t 
  ON m.hometeam_id = t.team_api_id),
away AS (
  SELECT m.id, m.date, t.team_long_name AS awayteam, m.away_goal
  FROM match AS m
  LEFT JOIN team AS t 
  ON m.awayteam_id = t.team_api_id)
SELECT 
	home.date,
    home.hometeam,
    away.awayteam,
    home.home_goal,
    away.away_goal
FROM home
INNER JOIN away
ON home.id = away.id;
```
#### The match is OVER
1. Select the match ID, country name, season, home, and away goals from the match and country tables. Complete the query that calculates the average number of goals scored overall and then includes the aggregate value in each row using a window function.
```
SELECT m.id , c.name AS country, m.season, m.home_goal, m.away_goal,
	AVG(m.home_goal + m.away_goal) OVER() AS overall_avg
FROM match AS m
LEFT JOIN country AS c ON m.country_id = c.id;
```
#### What's OVER here?
1. Select the league name and average total goals scored from league and match.
Complete the window function so it calculates the rank of average goals scored across all leagues in the database. Order the rank by the average total of home and away goals scored.
```
SELECT name AS league,
    AVG(m.home_goal + m.away_goal) AS avg_goals,
    RANK() OVER(ORDER BY AVG(m.home_goal + m.away_goal)) AS league_rank
FROM league AS l
LEFT JOIN match AS m 
ON l.id = m.country_id
WHERE m.season = '2011/2012'
GROUP BY l.name
ORDER BY league_rank;
```
#### Flip OVER your results
1. Complete the same parts of the query as the previous exercise.
Complete the window function to rank each league from highest to lowest average goals scored. Order the main query by the rank you just created.
```
SELECT name AS league,
    AVG(m.home_goal + m.away_goal) AS avg_goals,
    RANK() OVER(ORDER BY AVG(m.home_goal + m.away_goal) DESC) AS league_rank
FROM league AS l
LEFT JOIN match AS m 
ON l.id = m.country_id
WHERE m.season = '2011/2012'
GROUP BY l.name
ORDER BY league_rank;
```
#### PARTITION BY a column
1. Complete the two window functions that calculate the home and away goal averages. Partition the window functions by season to calculate separate averages for each season. Filter the query to only include matches played by Legia Warszawa, id = 8673.
```
SELECT date, season, home_goal, away_goal,
    CASE WHEN hometeam_id = 8673 THEN 'home' 
         ELSE 'away' END AS warsaw_location,
    AVG(home_goal) OVER(PARTITION BY season) AS season_homeavg,
    AVG(away_goal) OVER(PARTITION BY season) AS season_awayavg
FROM match
WHERE hometeam_id = 8673 OR awayteam_id = 8673
ORDER BY (home_goal + away_goal) DESC;
```
#### PARTITION BY multiple columns
1. Construct two window functions partitioning the average of home and away goals by season and month. Filter the dataset by Legia Warszawa's team ID (8673) so that the window calculation only includes matches involving them.
```
SELECT date, season, home_goal, away_goal,
	CASE WHEN hometeam_id = 8673 THEN 'home' 
         ELSE 'away' END AS warsaw_location,
    AVG(home_goal) OVER(PARTITION BY season, 
         	EXTRACT(month FROM date)) AS season_mo_home,
    AVG(away_goal) OVER(PARTITION BY season, 
            EXTRACT(month FROM date)) AS season_mo_away
FROM match
WHERE 
	hometeam_id = '8673'
    OR awayteam_id = '8673'
ORDER BY (home_goal + away_goal) DESC;
```
#### Slide to the left
1. Complete the window function by:
Assessing the running total of home goals scored by FC Utrecht.
Assessing the running average of home goals scored.
Ordering both the running average and running total by date.

```
SELECT date, home_goal, away_goal,
    SUM(home_goal) OVER(ORDER BY date 
         ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS running_total,
    AVG(home_goal) OVER(ORDER BY date 
         ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS running_avg
FROM match
WHERE 
	hometeam_id = 9908 
	AND season = '2011/2012';
```
#### Slide to the right
1. Complete the window function by:
Assessing the running total of home goals scored by FC Utrecht.
Assessing the running average of home goals scored.
Ordering both the running average and running total by date, descending.

```
SELECT date, home_goal, away_goal,
    SUM(home_goal) OVER(ORDER BY date DESC
         ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING) AS running_total,
    AVG(home_goal) OVER(ORDER BY date DESC
         ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING) AS running_avg
FROM match
WHERE 
	awayteam_id = 9908 
    AND season = '2011/2012';
```
#### Setting up the home team CTE
1. Create a CASE statement that identifies each match as a win, lose, or tie for Manchester United.
Fill out the logical operators for each WHEN clause in the CASE statement (equals, greater than, less than).
Join the tables on home team ID from match, and team_api_id from team.
Filter the query to only include games from the 2014/2015 season where Manchester United was the home team.

```
SELECT m.id, t.team_long_name,
	CASE WHEN m.home_goal > m.away_goal THEN 'MU Win'
		 WHEN m.home_goal < m.away_goal THEN 'MU Loss'
        ELSE 'Tie' END AS outcome
FROM match AS m
LEFT JOIN team AS t 
ON m.hometeam_id = t.team_api_id
WHERE season = '2014/2015'
	AND t.team_long_name = 'Manchester United';
```

#### Setting up the away team CTE
1. Complete the CASE statement syntax. Fill out the logical operators identifying each match as a win, loss, or tie for Manchester United. Join the table on awayteam_id, and team_api_id.

```
SELECT m.id, t.team_long_name,
	CASE WHEN m.home_goal > m.away_goal THEN 'MU Loss'
		WHEN m.home_goal < m.away_goal THEN 'MU Win'
        ELSE 'Tie' END AS outcome
FROM match AS m
LEFT JOIN team AS t 
ON m.awayteam_id = t.team_api_id
WHERE m.season = '2014/2015'
	AND t.team_long_name = 'Manchester United';
```

#### Putting the CTEs together
1. Declare the home and away CTEs before your main query. Join your CTEs to the match table using a LEFT JOIN. Select the relevant data from the CTEs into the main query. Select the date from match, team names from the CTEs, and home/ away goals from match in the main query.

```
WITH home AS (
  SELECT m.id, t.team_long_name,
	  CASE WHEN m.home_goal > m.away_goal THEN 'MU Win'
		   WHEN m.home_goal < m.away_goal THEN 'MU Loss' 
  		   ELSE 'Tie' END AS outcome
  FROM match AS m
  LEFT JOIN team AS t ON m.hometeam_id = t.team_api_id),
away AS (
  SELECT m.id, t.team_long_name,
	  CASE WHEN m.home_goal > m.away_goal THEN 'MU Loss'
		   WHEN m.home_goal < m.away_goal THEN 'MU Win' 
  		   ELSE 'Tie' END AS outcome
  FROM match AS m
  LEFT JOIN team AS t ON m.awayteam_id = t.team_api_id)
SELECT DISTINCT
    m.date,
    home.team_long_name AS home_team,
    away.team_long_name AS away_team,
    m.home_goal, m.away_goal
-- Join the CTEs onto the match table
FROM match AS m
LEFT JOIN home ON m.id = home.id
LEFT JOIN away ON m.id = away.id
WHERE m.season = '2014/2015'
      AND (home.team_long_name = 'Manchester United' 
           OR away.team_long_name = 'Manchester United');
```

#### Add a window function
1. Set up the CTEs so that the home and away teams each have a name, ID, and score associated with them. Select the date, home team name, away team name, home goal, and away goals scored in the main query. Rank the matches and order by the difference in scores in descending order.
```
WITH home AS (
  SELECT m.id, t.team_long_name,
	  CASE WHEN m.home_goal > m.away_goal THEN 'MU Win'
		   WHEN m.home_goal < m.away_goal THEN 'MU Loss' 
  		   ELSE 'Tie' END AS outcome
  FROM match AS m
  LEFT JOIN team AS t ON m.hometeam_id = t.team_api_id),
away AS (
  SELECT m.id, t.team_long_name,
	  CASE WHEN m.home_goal > m.away_goal THEN 'MU Loss'
		   WHEN m.home_goal < m.away_goal THEN 'MU Win' 
  		   ELSE 'Tie' END AS outcome
  FROM match AS m
  LEFT JOIN team AS t ON m.awayteam_id = t.team_api_id)
SELECT DISTINCT
    m.date,
    home.team_long_name AS home_team,
    away.team_long_name AS away_team,
    m.home_goal, m.away_goal,
    RANK() OVER(ORDER BY ABS(home_goal - away_goal) DESC) as match_rank
FROM match AS m
LEFT JOIN home ON m.id = home.id
RIGHT JOIN away ON m.id = away.id
WHERE m.season = '2014/2015'
      AND ((home.team_long_name = 'Manchester United' AND home.outcome = 'MU Loss')
      OR (away.team_long_name = 'Manchester United' AND away.outcome = 'MU Loss'));
```

## PostgreSQL Summary Stats and Window Function

### Introduction to window functions

#### Numbering rows
1. Number each row in the dataset.
```
SELECT
  *, ROW_NUMBER()OVER() AS Row_N
FROM Summer_Medals
ORDER BY Row_N ASC;
```
#### Numbering Olympic games in ascending order
1. Assign a number to each year in which Summer Olympic games were held.
```
SELECT Year, ROW_NUMBER() OVER() AS Row_N
FROM (
  SELECT DISTINCT Year
  FROM Summer_Medals
  ORDER BY Year ASC) AS Years
ORDER BY Year ASC;
```
#### Numbering Olympic games in descending order
1. Assign a number to each year in which Summer Olympic games were held so that rows with the most recent years have lower row numbers.
```
SELECT Year, ROW_NUMBER() OVER (ORDER BY Year DESC) AS Row_N
FROM (
  SELECT DISTINCT Year
  FROM Summer_Medals
) AS Years
ORDER BY Year;
```
#### Numbering Olympic athletes by medals earned
1. For each athlete, count the number of medals he or she has earned.
```
SELECT athlete,
  COUNT(medal) AS Medals
FROM Summer_Medals
GROUP BY Athlete
ORDER BY Medals DESC;
```
2. Having wrapped the previous query in the Athlete_Medals CTE, rank each athlete by the number of medals they've earned.
```
SELECT athlete,
  ROW_NUMBER() OVER (ORDER BY Medals DESC) AS Row_N
FROM Athlete_Medals
ORDER BY Medals DESC;
```
#### Reigning weightlifting champions
1. Return each year's gold medalists in the Men's 69KG weightlifting competition.
```
SELECT year, country AS champion
FROM Summer_Medals
WHERE
  Discipline = 'Weightlifting' AND
  Event = '69KG' AND
  Gender = 'Men' AND
  Medal = 'Gold';
```
2. Having wrapped the previous query in the Weightlifting_Gold CTE, get the previous year's champion for each year.
```
SELECT
  Year, Champion, LAG(Champion) OVER
    (ORDER BY year ASC) AS Last_Champion
FROM Weightlifting_Gold
ORDER BY Year ASC;
```
#### Reigning champions by gender
1. Return the previous champions of each year's event by gender.
```
WITH Tennis_Gold AS (
  SELECT DISTINCT
    Gender, Year, Country
  FROM Summer_Medals
  WHERE
    Year >= 2000 AND
    Event = 'Javelin Throw' AND
    Medal = 'Gold')
SELECT
  Gender, Year,
  Country AS Champion,
  LAG(Country) OVER (PARTITION BY Gender ORDER BY Year ASC) AS Last_Champion
FROM Tennis_Gold
ORDER BY Gender ASC, Year ASC;
```
#### Reigning champions by gender and event
1. Return the previous champions of each year's events by gender and event.
```
WITH Athletics_Gold AS (
  SELECT DISTINCT
    Gender, Year, Event, Country
  FROM Summer_Medals
  WHERE
    Year >= 2000 AND
    Discipline = 'Athletics' AND
    Event IN ('100M', '10000M') AND
    Medal = 'Gold')

SELECT
  Gender, Year, Event,
  Country AS Champion, LAG(Country) OVER (PARTITION BY Gender, Event ORDER BY Year ASC) AS Last_Champion
FROM Athletics_Gold
ORDER BY Event ASC, Gender ASC, Year ASC;
```

### Fetching, ranking, and paging
#### Future gold medalist
1. For each year, fetch the current gold medalist and the gold medalist 3 competitions ahead of the current row.
```
WITH Discus_Medalists AS (
  SELECT DISTINCT
    Year,
    Athlete
  FROM Summer_Medals
  WHERE Medal = 'Gold'
    AND Event = 'Discus Throw'
    AND Gender = 'Women'
    AND Year >= 2000)

SELECT Year, athlete,
  LEAD(athlete, 3) OVER (ORDER BY year ASC) AS Future_Champion
FROM Discus_Medalists
ORDER BY Year ASC;
```
#### First athlete by name
1. Return all athletes and the first athlete ordered by alphabetical order.
```
WITH All_Male_Medalists AS (
  SELECT DISTINCT
    Athlete
  FROM Summer_Medals
  WHERE Medal = 'Gold'
    AND Gender = 'Men')

SELECT Athlete,
  FIRST_VALUE(Athlete) OVER (
    ORDER BY Athlete ASC
  ) AS First_Athlete
FROM All_Male_Medalists;
```
#### Last country by name
1. Return the year and the city in which each Olympic games were held. Fetch the last city in which the Olympic games were held.
```
WITH Hosts AS (
  SELECT DISTINCT Year, City
    FROM Summer_Medals)

SELECT
  Year,
  City, LAST_VALUE(City) OVER (
   ORDER BY Year ASC
   RANGE BETWEEN
     UNBOUNDED PRECEDING AND
     UNBOUNDED FOLLOWING
  ) AS Last_City
FROM Hosts
ORDER BY Year ASC;
```
#### Ranking athletes by medals earned
1. Rank each athlete by the number of medals they've earned -- the higher the count, the higher the rank -- with identical numbers in case of identical values.
```
WITH Athlete_Medals AS (
  SELECT
    Athlete,
    COUNT(*) AS Medals
  FROM Summer_Medals
  GROUP BY Athlete)
SELECT
  Athlete,
  Medals,
  RANK() OVER (ORDER BY Medals DESC) AS Rank_N
FROM Athlete_Medals
ORDER BY Medals DESC;
```
#### Ranking athletes from multiple countries
1. Rank each country's athletes by the count of medals they've earned -- the higher the count, the higher the rank -- without skipping numbers in case of identical values.
```
WITH Athlete_Medals AS (
  SELECT
    Country, Athlete, COUNT(*) AS Medals
  FROM Summer_Medals
  WHERE
    Country IN ('JPN', 'KOR')
    AND Year >= 2000
  GROUP BY Country, Athlete
  HAVING COUNT(*) > 1)
SELECT
  Country, Athlete,
  DENSE_RANK() OVER (PARTITION BY Country ORDER BY Medals DESC) AS Rank_N
FROM Athlete_Medals
ORDER BY Country ASC, RANK_N ASC;
```
#### Paging events
1.Split the distinct events into exactly 111 groups, ordered by event in alphabetical order.
```
WITH Events AS (
  SELECT DISTINCT Event
  FROM Summer_Medals)
SELECT Event,
  NTILE(111) OVER (ORDER BY Event ASC) AS Page
FROM Events
ORDER BY Event ASC;
```
#### Top, middle, and bottom thirds
1. Split the athletes into top, middle, and bottom thirds based on their count of medals.
```
WITH Athlete_Medals AS (
  SELECT Athlete, COUNT(*) AS Medals
  FROM Summer_Medals
  GROUP BY Athlete
  HAVING COUNT(*) > 1)
  
SELECT Athlete, Medals,
  NTILE(3) OVER(ORDER BY Medals DESC) AS Third
FROM Athlete_Medals
ORDER BY Medals DESC, Athlete ASC;
```
2. Return the average of each third.
```
WITH Athlete_Medals AS (
  SELECT Athlete, COUNT(*) AS Medals
  FROM Summer_Medals
  GROUP BY Athlete
  HAVING COUNT(*) > 1),
  
  Thirds AS (
  SELECT
    Athlete,
    Medals,
    NTILE(3) OVER (ORDER BY Medals DESC) AS Third
  FROM Athlete_Medals)

SELECT
  Third,
  AVG(Medals) AS Avg_Medals
FROM Thirds
GROUP BY Third
ORDER BY Third ASC;
```
### Aggregate window functions and frames
#### Running totals of athlete medals
#### Maximum country medals by year
#### Minimum country medals by year
#### Moving maximum of Scandinavian athletes' medals
#### Moving maximum of Chinese athletes' medals
#### Moving average of Russian medals
#### Moving total of countries' medals

## Functions for Manipulating Data in PostgreSQL
### Overview of Common Data Types
#### Getting information about your database
1. Select all columns from the INFORMATION_SCHEMA.TABLES system database. Limit results that have a public table_schema. 

```
SELECT * 
FROM INFORMATION_SCHEMA.TABLES
WHERE table_schema = 'public';
```
2. Select all columns from the INFORMATION_SCHEMA.COLUMNS system database. Limit by table_name to actor.

```
SELECT * 
FROM INFORMATION_SCHEMA.COLUMNS 
WHERE table_name = 'actor';
```
#### Determing data types
1. Select the column name and data type from the INFORMATION_SCHEMA.COLUMNS system database. Limit results to only include the customer table.

```
SELECT column_name, data_type
FROM INFORMATION_SCHEMA.COLUMNS 
WHERE table_name = 'customer';
```
#### Interval data types
1. Select the rental date and return date from the rental table. Add an INTERVAL of 3 days to the rental_date to calculate the expected return date. 

```
SELECT rental_date, return_date, rental_date + INTERVAL '3 days' AS expected_return_date
FROM rental;
```

#### Accessing data in an ARRAY
1. Select the title and special features from the film table and compare the results between the two columns.
```
SELECT title, special_features
FROM film;
```
2. Select all films that have a special feature Trailers by filtering on the first Index of the special_features ARRAY.
```
SELECT title, special_features 
FROM film
WHERE special_features [1] = 'Trailers';
```
3. Now let's select all films that have Deleted Scenes in the second Index of the special_features ARRAY.
```
SELECT title, special_features 
FROM film
WHERE special_features[2] = 'Deleted Scenes';

```

#### Searching an ARRAY with ANY
1. Match 'Trailers' in any Index of the special_features ARRAY regardless of position.
```
SELECT title, special_features 
FROM film 
WHERE 'Trailers' = ANY (special_features);
```

#### Searching an ARRAY with @>
1. Use the containa operator to match the text Deleted Scenes in the special_features column.
```
SELECT title, special_features 
FROM film 
WHERE special_features @> ARRAY['Deleted Scenes'];
```
### Working with DATE/TIME Functions and Operators
#### Adding and subtracting dat and time values
1. Subtract the rental_date from the return_date to calculate the number of days_rented.
```
SELECT f.title, f.rental_duration, r.return_date - r.rental_date AS days_rented
FROM film AS f
     INNER JOIN inventory AS i ON f.film_id = i.film_id
     INNER JOIN rental AS r ON i.inventory_id = r.inventory_id
ORDER BY f.title;
```
2. Now use the AGE() function to calculate the days_rented.
```
SELECT f.title, f.rental_duration, AGE(r.return_date, r.rental_date) AS days_rented
FROM film AS f
	INNER JOIN inventory AS i ON f.film_id = i.film_id
	INNER JOIN rental AS r ON i.inventory_id = r.inventory_id
ORDER BY f.title;
```
#### INTERVAL arithmetic
1. Convert rental_duration by multiplying it with a 1 day INTERVAL. Subtract the rental_date from the return_date to calculate the number of days_rented. Exclude rentals with a NULL value for return_date.
```
SELECT
    f.title,
    INTERVAL '1' day * f.rental_duration, r.return_date - r.rental_date AS days_rented
FROM film AS f
    INNER JOIN inventory AS i ON f.film_id = i.film_id
    INNER JOIN rental AS r ON i.inventory_id = r.inventory_id
WHERE r.return_date IS NOT NULL
ORDER BY f.title;
```
#### Calculating the expected return date
1. Convert rental_duration by multiplying it with a 1-day INTERVAL. Add it to the rental date.
```
SELECT
    f.title,
	r.rental_date,
    f.rental_duration, interval '1' day * f.rental_duration + r.rental_date AS expected_return_date, r.return_date
FROM film AS f
    INNER JOIN inventory AS i ON f.film_id = i.film_id
    INNER JOIN rental AS r ON i.inventory_id = r.inventory_id
ORDER BY f.title;
```

















