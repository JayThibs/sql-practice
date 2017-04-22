# [SQLZoo Tutorial Solutions](http://sqlzoo.net/wiki/SQL_Tutorial)

## [More JOIN operations](https://sqlzoo.net/wiki/More_JOIN_operations)

### 1. List the films where the yr is 1962 [Show id, title]
```sh
SELECT id, title
 FROM movie
 WHERE yr=1962
```
### 2. Give year of 'Citizen Kane'.
```sh
SELECT yr
FROM movie
WHERE title = 'Citizen Kane'
```
### 3. List all of the Star Trek movies, include the id, title and yr (all of these movies include the words Star Trek in the title). Order results by year.
```sh
SELECT id, title, yr
FROM movie
WHERE title LIKE '%Star Trek%'
ORDER BY yr;
```
### 4: What id number does the actor 'Glenn Close' have?
```sh
SELECT id
FROM actor
WHERE name = 'Glenn Close'
```
### 5. What is the id of the film 'Casablanca'
```sh
SELECT id
FROM movie
WHERE title = 'Casablanca'
```
### 6. Obtain the cast list for 'Casablanca'.
```sh
SELECT name
FROM actor JOIN casting ON id = actorid
WHERE movieid=11768
```
### 7. Obtain the cast list for the film 'Alien'
```sh
SELECT name
FROM  actor JOIN casting 
ON actor.id = casting.actorid 
JOIN movie 
ON movie.id = casting.movieid
WHERE movie.title = 'Alien';
```
### 8. List the films in which 'Harrison Ford' has appeared
```sh
SELECT movie.title
FROM movie JOIN casting ON movie.id = casting.movieid
JOIN actor ON actor.id = casting.actorid
WHERE actor.name = 'Harrison Ford';
```
### 9. List the films where 'Harrison Ford' has appeared - but not in the starring role. 
```sh
SELECT title
FROM movie JOIN casting ON movie.id = casting.movieid
JOIN actor ON casting.actorid = actor.id
WHERE name = 'Harrison Ford' AND ord!=1
```
### 10. List the films together with the leading star for all 1962 films.
```sh
SELECT title, name
FROM movie JOIN casting ON movie.id = casting.movieid
JOIN actor ON casting.actorid = actor.id
WHERE yr = 1962 AND ord = 1
```
### 11. Which were the busiest years for 'John Travolta', show the year and the number of movies he made each year for any year in which he made more than 2 movies.
```sh
SELECT yr, COUNT(title) 
FROM movie JOIN casting ON movie.id=movieid
JOIN actor ON actorid=actor.id
WHERE name = 'John Travolta'
GROUP BY yr
HAVING COUNT(title) > 2
```
### 12. List the film title and the leading actor for all of the films 'Julie Andrews' played in.
```sh
SELECT movie.title, actor.name 
FROM movie JOIN casting ON movie.id = casting.movieid
JOIN actor ON actor.id = casting.actorid
WHERE movieid IN (SELECT movieid FROM casting WHERE actorid IN (SELECT actor.id FROM actor
  WHERE name='Julie Andrews'))
AND
ord = 1
```
### 13. Obtain a list, in alphabetical order, of actors who've had at least 30 starring roles.
```sh
SELECT name
FROM movie JOIN casting ON movie.id = casting.movieid
JOIN actor ON actor.id = casting.actorid
WHERE ord = 1
GROUP BY name
HAVING COUNT(name) >= 30
ORDER BY name
```
### 14. List the films released in the year 1978 ordered by the number of actors in the cast, then by title. 
```sh
SELECT movie.title, COUNT(*)
FROM movie JOIN casting ON movie.id = casting.movieid
WHERE yr = 1978
GROUP BY movie.title
ORDER BY COUNT(*) DESC, title
```
### 15. List all the people who have worked with 'Art Garfunkel'.
```sh
SELECT ArtCoActors.name
  FROM (SELECT movie.*
          FROM movie
          JOIN casting
            ON casting.movieid = movie.id
          JOIN actor
            ON actor.id = casting.actorid
         WHERE actor.name = 'Art Garfunkel') AS ArtMovies
  JOIN (SELECT actor.*, casting.movieid
          FROM actor
          JOIN casting
            ON casting.actorid = actor.id
         WHERE actor.name != 'Art Garfunkel') AS ArtCoActors
    ON ArtMovies.id = ArtCoActors.movieid;
```
