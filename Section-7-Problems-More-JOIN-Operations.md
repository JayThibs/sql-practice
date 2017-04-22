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
