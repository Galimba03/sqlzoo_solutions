# SQLZOO Solutions
I've completed all the problems on the [SQLZOO Tutoral](http://sqlzoo.net/wiki/SQL_Tutorial).
This was done because of my course of 'Data Bases 1'. Enjoy!

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

## SELECT from nobel
1. 