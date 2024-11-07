# SQLZOO Solutions

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
1. Show the total population of the world.
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
1. Modify it to show the matchid and player name for all goals scored by Germany. To identify German players, check for: teamid = 'GER'
```sql
SELECT matchid, player
FROM goal 
WHERE teamid='GER'
```

2. Show id, stadium, team1, team2 for just game 1012
```sql
SELECT id, stadium, team1, team2
FROM game
WHERE id=1012
```

3. Modify it to show the player, teamid, stadium and mdate for every German goal.
```sql
SELECT player, teamid, stadium, mdate
FROM game INNER JOIN goal ON id=matchid
WHERE teamid='GER'
```

4. Show the team1, team2 and player for every goal scored by a player called Mario player LIKE 'Mario%'
```sql
SELECT team1, team2, player
FROM game INNER JOIN goal ON game.id=goal.matchid
WHERE player LIKE 'Mario%'
```

5. Show player, teamid, coach, gtime for all goals scored in the first 10 minutes gtime<=10
```sql
SELECT player, teamid, coach, gtime
FROM goal INNER JOIN eteam ON goal.teamid=eteam.id
WHERE gtime<=10
```

6. List the dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach.
```sql
SELECT mdate, teamname
FROM game INNER JOIN eteam ON game.team1=eteam.id
WHERE coach='Fernando Santos'
```

7. List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'
```sql
SELECT player
FROM goal INNER JOIN game ON goal.matchid=game.id
WHERE stadium='National Stadium, Warsaw'
```

8. Instead show the name of all players who scored a goal against Germany.
```sql
SELECT DISTINCT player
FROM game JOIN goal ON game.id=goal.matchid
WHERE teamid!='GER' AND (team1='GER' OR team2='GER')
```

9. Show teamname and the total number of goals scored.
```sql
SELECT teamname, COUNT(matchid)
FROM eteam INNER JOIN goal ON eteam.id=goal.teamid
GROUP BY teamname
```

10. Show the stadium and the number of goals scored in each stadium.
```sql
SELECT stadium, COUNT(matchid)
FROM game INNER JOIN goal ON game.id=goal.matchid
GROUP BY stadium
```

11. For every match involving 'POL', show the matchid, date and the number of goals scored.
```sql
SELECT matchid, mdate, COUNT(matchid)
FROM game INNER JOIN goal ON matchid = id 
WHERE (team1='POL' OR team2='POL')
GROUP BY matchid, mdate
```

12. For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'
```sql
SELECT matchid, mdate, COUNT(matchid)
FROM goal INNER JOIN game ON goal.matchid=game.id
WHERE teamid='GER'
GROUP BY matchid, mdate
```

13. List every match with the goals scored by each team as shown. This will use "CASE WHEN" which has not been explained in any previous exercises.
```sql
SELECT DISTINCT mdate, team1, SUM(CASE WHEN teamid=team1 THEN 1 ELSE 0 END) AS score1, team2, SUM(CASE WHEN teamid=team2 THEN 1 ELSE 0 END) AS score2
FROM game LEFT JOIN goal ON game.id = goal.matchid
GROUP BY id, mdate, team1, team2
ORDER BY mdate, matchid, team1, team2
```

---

## More JOIN
1. List the films where the yr is 1962 [Show id, title]
```sql
SELECT id, title
FROM movie
WHERE yr=1962
```

2. Give year of 'Citizen Kane'.
```sql
SELECT yr
FROM movie
WHERE title='Citizen Kane'
```

3. List all of the Star Trek movies, include the id, title and yr (all of these movies include the words Star Trek in the title). Order results by year.
```sql
SELECT id, title, yr
FROM movie
WHERE title LIKE '%Star Trek%'
ORDER BY yr
```

4. What id number does the actor 'Glenn Close' have?
```sql
SELECT id
FROM actor
WHERE name = 'Glenn Close'
```

5. What is the id of the film 'Casablanca'
```sql
SELECT id
FROM movie
WHERE title='Casablanca'
```

6. Obtain the cast list for 'Casablanca'.
```sql
SELECT name
FROM movie INNER JOIN casting ON movie.id=casting.movieid
 INNER JOIN actor ON casting.actorid=actor.id
WHERE movieid=11768
```

7. Obtain the cast list for the film 'Alien'
```sql
SELECT name
FROM movie INNER JOIN casting ON movie.id=casting.movieid
 INNER JOIN actor ON casting.actorid=actor.id
WHERE title='Alien'
```

8. List the films in which 'Harrison Ford' has appeared
```sql
SELECT title
FROM movie INNER JOIN casting ON movie.id=casting.movieid
 INNER JOIN actor ON casting.actorid=actor.id
WHERE name='Harrison Ford'
```

9. List the films where 'Harrison Ford' has appeared - but not in the starring role. [Note: the ord field of casting gives the position of the actor. If ord=1 then this actor is in the starring role]
```sql
SELECT title
FROM movie INNER JOIN casting ON movie.id=casting.movieid
 INNER JOIN actor ON casting.actorid=actor.id
WHERE name='Harrison Ford' AND ord!=1
```

10. List the films together with the leading star for all 1962 films.
```sql
SELECT title, name
FROM movie INNER JOIN casting ON movie.id=casting.movieid
 INNER JOIN actor ON casting.actorid=actor.id
WHERE yr=1962 AND ord=1
```

11. Which were the busiest years for 'Rock Hudson', show the year and the number of movies he made each year for any year in which he made more than 2 movies.
```sql
SELECT yr,COUNT(title) 
FROM movie INNER JOIN casting ON movie.id=movieid
 INNER JOIN actor ON actorid=actor.id
WHERE name='Rock Hudson'
GROUP BY yr
HAVING COUNT(title) > 2
```

12. List the film title and the leading actor for all of the films 'Julie Andrews' played in.
```sql
SELECT title, name 
FROM casting INNER JOIN movie ON movie.id = movieid
 INNER JOIN actor ON actor.id = actorid
WHERE ord = 1 AND movie.id IN
 (SELECT movie.id FROM movie
 INNER JOIN casting ON movie.id = movieid
 INNER JOIN actor ON actor.id = actorid
 WHERE actor.name = 'Julie Andrews')
```

13. Obtain a list, in alphabetical order, of actors who've had at least 15 starring roles.
```sql
SELECT DISTINCT name
FROM casting INNER JOIN movie ON movie.id = movieid
 INNER JOIN actor ON actor.id = actorid
WHERE actorid IN
 (SELECT actorid
 FROM casting
 WHERE ord = 1
 GROUP BY actorid
 HAVING COUNT(actorid) >= 15)
ORDER BY name
```

14. List the films released in the year 1978 ordered by the number of actors in the cast, then by title.
```sql
SELECT title, COUNT(actorid)
FROM movie INNER JOIN casting ON movie.id=casting.movieid
WHERE yr=1978
GROUP BY title
ORDER BY COUNT(actorid) DESC, title
```

15. List all the people who have worked with 'Art Garfunkel'.
```sql
SELECT DISTINCT name 
FROM casting INNER JOIN actor ON actorid = actor.id
WHERE name != 'Art Garfunkel' AND movieid IN
 (SELECT movieid
 FROM movie INNER JOIN casting ON movieid = movie.id
 INNER JOIN actor ON actorid = actor.id
 WHERE actor.name = 'Art Garfunkel')
```

---

## Using NULL
1. List the teachers who have NULL for their department.
```sql
SELECT name
FROM teacher
WHERE dept IS null
```

2. Note the INNER JOIN misses the teachers with no department and the departments with no teacher.
```sql
SELECT teacher.name, dept.name
FROM teacher INNER JOIN dept ON (teacher.dept=dept.id)
```

3. Use a different JOIN so that all teachers are listed.
```sql
SELECT teacher.name, dept.name
FROM teacher LEFT JOIN dept ON teacher.dept=dept.id
```

4. Use a different JOIN so that all departments are listed.
```sql
SELECT teacher.name, dept.name
FROM teacher RIGHT JOIN dept ON teacher.dept=dept.id
```

5. Show teacher name and mobile number or '07986 444 2266'
```sql
SELECT name, COALESCE(mobile, '07986 444 2266')
FROM teacher
```

6. Use the COALESCE function and a LEFT JOIN to print the teacher name and department name. Use the string 'None' where there is no department.
```sql
SELECT teacher.name, COALESCE(dept.name,'None')
FROM teacher LEFT JOIN dept ON teacher.dept = dept.id
```

7. Use COUNT to show the number of teachers and the number of mobile phones.
```sql
SELECT COUNT(name), COUNT(mobile)
FROM teacher
```

8. Use COUNT and GROUP BY dept.name to show each department and the number of staff. Use a RIGHT JOIN to ensure that the Engineering department is listed.
```sql
SELECT dept.name, COUNT(teacher.name)
FROM teacher RIGHT JOIN dept ON teacher.dept=dept.id
GROUP BY dept
ORDER BY dept.name
```

9. Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2 and 'Art' otherwise.
```sql
SELECT name, CASE WHEN dept IN (1,2) THEN 'Sci' ELSE 'Art' END
FROM teacher
```

10. Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2, show 'Art' if the teacher's dept is 3 and 'None' otherwise. 
```sql
SELECT name, CASE WHEN dept IN (1,2) THEN 'Sci' WHEN dept = 3 THEN 'Art' ELSE 'None' END
FROM teacher
```

---

## Self JOIN
1. How many stops are in the database.
```sql
SELECT COUNT(id)
FROM stops
```

2. Find the id value for the stop 'Craiglockhart'
```sql
SELECT id
FROM stops
WHERE name='Craiglockhart'
```

3. Give the id and the name for the stops on the '4' 'LRT' service.
```sql
SELECT id, name 
FROM stops INNER JOIN route ON stops.id=route.stop
WHERE company='LRT' AND num=4
```

4. The query shown gives the number of routes that visit either London Road (149) or Craiglockhart (53). Run the query and notice the two services that link these stops have a count of 2. Add a HAVING clause to restrict the output to these two routes.
```sql
SELECT company, num, COUNT(*)
FROM route WHERE stop=149 OR stop=53
GROUP BY company, num
HAVING COUNT(*)>=2
```

5. Execute the self join shown and observe that b.stop gives all the places you can get to from Craiglockhart, without changing routes. Change the query so that it shows the services from Craiglockhart to London Road.
```sql
SELECT a.company, a.num, a.stop, b.stop
FROM route a JOIN route b ON (a.company=b.company AND a.num=b.num)
WHERE a.stop=53 AND b.stop=149
```

6. The query shown is similar to the previous one, however by joining two copies of the stops table we can refer to stops by name rather than by number. Change the query so that the services between 'Craiglockhart' and 'London Road' are shown. If you are tired of these places try 'Fairmilehead' against 'Tollcross'
```sql
SELECT a.company, a.num, stopa.name, stopb.name
FROM route a INNER JOIN route b ON (a.company=b.company AND a.num=b.num)
 INNER JOIN stops stopa ON (a.stop=stopa.id)
 INNER JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Craiglockhart' AND stopb.name='London Road'
```

7. Give a list of all the services which connect stops 115 and 137 ('Haymarket' and 'Leith')
```sql
SELECT a.company, a.num  
FROM route a JOIN route b ON a.num = b.num
WHERE a.stop = 115 AND b.stop = 137
GROUP BY num
```

8. Give a list of the services which connect the stops 'Craiglockhart' and 'Tollcross'
```sql
SELECT a.company, a.num
FROM route a INNER JOIN route b ON (a.num = b.num)
 INNER JOIN stops stopa ON (a.stop = stopa.id)
 INNER JOIN stops stopb ON (b.stop = stopb.id)
WHERE stopa.name='Craiglockhart' AND stopb.name='Tollcross'
```

9. Give a distinct list of the stops which may be reached from 'Craiglockhart' by taking one bus, including 'Craiglockhart' itself, offered by the LRT company. Include the company and bus no. of the relevant services.
```sql
SELECT DISTINCT stopa.name, a.company, a.num
FROM route a INNER JOIN route b ON a.num=b.num
 INNER JOIN stops stopa ON stopa.id = a.stop
 INNER JOIN stops stopb ON stopb.id = b.stop
WHERE stopb.name='Craiglockhart' AND a.company='LRT'
```

10. Find the routes involving two buses that can go from Craiglockhart to Lochend.
Show the bus no. and company for the first bus, the name of the stop for the transfer,
and the bus no. and company for the second bus.
```sql
SELECT a.num, a.company, stopb.name, c.num, c.company
FROM route a INNER JOIN route b ON (a.company = b.company AND a.num = b.num)
 INNER JOIN (route c JOIN route d ON (c.company = d.company AND c.num = d.num))
 INNER JOIN stops stopa ON a.stop = stopa.id
 INNER JOIN stops stopb ON b.stop = stopb.id
 INNER JOIN stops stopc ON c.stop = stopc.id
 INNER JOIN stops stopd ON d.stop = stopd.id
WHERE stopa.name = 'Craiglockhart' AND stopd.name = 'Lochend' AND stopb.name = stopc.name
```