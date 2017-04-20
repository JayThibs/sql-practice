# [SQLZoo Tutorial Solutions](http://sqlzoo.net/wiki/SQL_Tutorial)

## [The JOIN operation](https://sqlzoo.net/wiki/The_JOIN_operation)

### 1. Modify it to show the matchid and player name for all goals scored by Germany. To identify German players, check for: teamid = 'GER'
```sh
SELECT matchid, player FROM goal 
  WHERE teamid = 'GER'
```
### 2: Show id, stadium, team1, team2 for just game 1012
```sh
SELECT id,stadium,team1,team2
  FROM game
WHERE id = '1012'
```
### 3: Modify it to show the player, teamid, stadium and mdate and for every German goal.
```sh
SELECT player, teamid, stadium, mdate
  FROM game JOIN goal ON (id=matchid)
WHERE teamid = 'GER'
```
### 4: Show the team1, team2 and player for every goal scored by a player called Mario player LIKE 'Mario%'
```sh
SELECT team1, team2, player
FROM game JOIN goal ON (id=matchid)
WHERE player LIKE 'Mario%'
```
### 5. Show player, teamid, coach, gtime for all goals scored in the first 10 minutes gtime<=10
```sh
SELECT player, teamid, coach, gtime
  FROM goal JOIN eteam on teamid=id
 WHERE gtime<=10
```
