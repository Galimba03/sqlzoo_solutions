# SQLZOO Solutions
I've completed all the problems on the [SQLZOO Tutoral](http://sqlzoo.net/wiki/SQL_Tutorial).<br>
This was done for educational purposes and I did it because I couldn't find any solutions on the website, so I thought that it would have helped.<br>
Enjoy!🫶🏻

## Sections:
1. [SELECT basics](#select-basics)
2. [SELECT from WORLD](#select-from-world)
3. [SELECT from NOBEL](#select-from-nobel)
4. [SELECT in SELECT](#select-in-select)
5. [SUM and COUNT](#sum-and-count)
6. [JOIN](#join)
7. [More JOIN](#more-join)
8. [Using NULL](#using-null)
9. [Self JOIN](#self-join)

## SELECT basics
1. Modify it to show the population of Germany
```sql
SELECT population
FROM world
WHERE name='Germany'
```

2. Show the name and the population for 'Sweden', 'Norway' and 'Denmark'.
```sql
SELECT name, population
FROM world
WHERE name IN ('Sweden', 'Norway', 'Denmark')
```

3. The example below shows countries with an area of 250,000-300,000 sq. km. Modify it to show the country and the area for countries with an area between 200,000 and 250,000.
```sql
SELECT name, area
FROM world
WHERE (area BETWEEN 200000 AND 250000)
```

---

## SELECT from WORLD
1. Observe the result of running this SQL command to show the name, continent and population of all countries.
```sql
SELECT name, continent, population 
FROM world
```

2. Show the name for the countries that have a population of at least 200 million. 200 million is 200000000, there are eight zeros.
```sql
SELECT name
FROM world
WHERE population>=200000000
```

3. Give the name and the per capita GDP for those countries with a population of at least 200 million.
```sql
SELECT name, (gdp/population)
FROM world
WHERE population>=200000000
```

4. Show the name and population in millions for the countries of the continent 'South America'. Divide the population by 1000000 to get population in millions.
```sql
SELECT name, (population/1000000)
FROM world
WHERE continent='South America'
```

5. Show the name and population for France, Germany, Italy
```sql
SELECT name, population
FROM world
WHERE name IN ('France', 'Germany', 'Italy')
```

6. Show the countries which have a name that includes the word 'United'
```sql
SELECT name
FROM world
WHERE name LIKE '%United%'
```

7. Show the countries that are big by area or big by population. Show name, population and area.
```sql
SELECT name, population, area
FROM world
WHERE area>=3000000 OR population>=250000000
```

8. Exclusive OR (XOR). Show the countries that are big by area (more than 3 million) or big by population (more than 250 million) but not both. Show name, population and area.
```sql
SELECT name, population, area
FROM world
WHERE (area>=3000000 OR population>=250000000) AND NOT (area>=3000000 AND population>=250000000)
```

9. Show the name and population in millions and the GDP in billions for the countries of the continent 'South America'. Use the ROUND function to show the values to two decimal places.
```sql
SELECT name, ROUND(population/1000000, 2), ROUND(gdp/1000000000, 2)
FROM world
WHERE continent='South America'
```

10. Show the name and per-capita GDP for those countries with a GDP of at least one trillion (1000000000000; that is 12 zeros). Round this value to the nearest 1000.
```sql
SELECT name, ROUND(gdp/population, -3)
FROM world
WHERE gdp>=1000000000000
```

11. Show the name and capital where the name and the capital have the same number of characters.
```sql
SELECT name, capital
FROM world
WHERE LENGTH(name)=LENGTH(capital)
```

12. Show the name and the capital where the first letters of each match. Don't include countries where the name and the capital are the same word.
```sql
SELECT name, capital
FROM world
WHERE LEFT(name, 1)=LEFT(capital, 1) AND name<>capital
```

13. Find the country that has all the vowels and no spaces in its name.
```sql
SELECT name
FROM world
WHERE (name LIKE '%a%') AND (name LIKE '%e%') AND (name LIKE '%i%') AND (name LIKE '%o%') AND (name LIKE '%u%') AND (name NOT LIKE '% %')
```

---

## SELECT from NOBEL
1. Change the query shown so that it displays Nobel prizes for 1950. 
```sql
SELECT yr, subject, winner
FROM nobel
WHERE yr=1950
```

2. Show who won the 1962 prize for literature.
```sql
SELECT winner
FROM nobel
WHERE yr=1962 AND subject='literature'
```

3. Show the year and subject that won 'Albert Einstein' his prize.
```sql
SELECT yr, subject
FROM nobel
WHERE winner='Albert Einstein'
```

4. Give the name of the 'peace' winners since the year 2000, including 2000.
```sql
SELECT winner
FROM nobel
WHERE yr>=2000 AND subject='peace'
```

5. Show all details (yr, subject, winner) of the literature prize winners for 1980 to 1989 inclusive.
```sql
SELECT yr, subject, winner
FROM nobel
WHERE subject='literature' AND (yr BETWEEN 1980 AND 1989)
```

6. Show all details of the presidential winners:
-  Theodore Roosevelt
-  Thomas Woodrow Wilson
-  Jimmy Carter
-  Barack Obama
```sql
SELECT yr, subject, winner
FROM nobel
WHERE winner IN ('Theodore Roosevelt', 'Thomas Woodrow Wilson', 'Jimmy Carter', 'Barack Obama')
```

7. Show the winners with first name John
```sql
SELECT winner
FROM nobel
WHERE winner LIKE 'John%'
```

8. Show the year, subject, and name of physics winners for 1980 together with the chemistry winners for 1984.
```sql
SELECT yr, subject, winner
FROM nobel
WHERE (subject='physics' AND yr=1980) OR (subject='chemistry' AND yr=1984)
```

9. Show the year, subject, and name of winners for 1980 excluding chemistry and medicine
```sql
SELECT yr, subject, winner
FROM nobel
WHERE (subject='physics' AND yr=1980) OR (subject='chemistry' AND yr=1984)
```

10. Show year, subject, and name of people who won a 'Medicine' prize in an early year (before 1910, not including 1910) together with winners of a 'Literature' prize in a later year (after 2004, including 2004)
```sql
SELECT yr, subject, winner
FROM nobel
WHERE (subject='medicine' AND yr<1910) OR (subject='literature' AND yr>=2004)
```
(bis) Just to know that exists the 'UNION' command. It's the logical union in Algebra
```sql
SELECT yr, subject, winner
FROM nobel
WHERE (subject='medicine' AND yr<1910)
UNION
SELECT yr, subject, winner
FROM nobel
WHERE (subject='literature' AND yr>=2004)
```

11. Find all details of the prize won by PETER GRÜNBERG.
-  Windows: Alt+1+5+4
-  MacOS: ⌥ Option+U and then U
```sql
SELECT *
FROM nobel
WHERE winner='Peter Grünberg'
```

12. Find all details of the prize won by EUGENE O'NEILL
```sql
SELECT *
FROM nobel
WHERE winner='Eugene O\'Neill'
```

13. List the winners, year and subject where the winner starts with Sir. Show the the most recent first, then by name order.
```sql
SELECT winner, yr, subject
FROM nobel
WHERE winner LIKE 'Sir%'
ORDER BY yr DESC, winner ASC
```

14. Show the 1984 winners and subject ordered by subject and winner name; but list chemistry and physics last.
```sql
SELECT winner, subject
FROM nobel
WHERE yr=1984
ORDER BY subject IN ('chemistry', 'physics'), subject, winner
```

---

## SELECT in SELECT
1. List each country name where the population is larger than that of 'Russia'.
```sql

```

2. Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.
```sql

```

3. List the name and continent of countries in the continents containing either Argentina or Australia. Order by name of the country.
```sql

```

4. Which country has a population that is more than United Kingdom but less than Germany? Show the name and the population.
```sql

```

5. Show the name and the population of each country in Europe. Show the population as a percentage of the population of Germany.
```sql

```

6. Which countries have a GDP greater than every country in Europe? [Give the name only.] (Some countries may have NULL gdp values)
```sql

```

7. Find the largest country (by area) in each continent, show the continent, the name and the area
```sql

```

8. List each continent and the name of the country that comes first alphabetically.
```sql

```

9. Find the continents where all countries have a population <= 25000000. Then find the names of the countries associated with these continents. Show name, continent and population.
```sql

```

10. Some countries have populations more than three times that of all of their neighbours (in the same continent). Give the countries and continents.
```sql

```

---

## SUM and COUNT
1. 1.
Show the total population of the world.
```sql
SELECT SUM(population)
FROM world
```

2. List all the continents - just once each.
```sql
SELECT DISTINCT continent
FROM world
```

3. Give the total GDP of Africa
```sql
SELECT SUM(gdp)
FROM world
WHERE continent='Africa'
```

4. How many countries have an area of at least 1000000
```sql
SELECT COUNT(name)
FROM world
WHERE area>=1000000
```

5. What is the total population of ('Estonia', 'Latvia', 'Lithuania')
```sql
SELECT SUM(population)
FROM world
WHERE name IN ('Estonia', 'Latvia', 'Lithuania')
```

6. For each continent show the continent and number of countries.
```sql
SELECT continent, COUNT(name)
FROM world
GROUP BY continent
```

7. For each continent show the continent and number of countries with populations of at least 10 million.
```sql
SELECT continent, COUNT(name)
FROM world
WHERE population>=10000000
GROUP BY continent
```

8. List the continents that have a total population of at least 100 million.
```sql
SELECT continent
FROM world
GROUP BY continent
HAVING SUM(population)>=100000000
```

---

## JOIN