# [SQLZoo Tutorial Solutions](http://sqlzoo.net/wiki/SQL_Tutorial)

## [The JOIN operation](https://sqlzoo.net/wiki/The_JOIN_operation)

### 1. Modify it to show the matchid and player name for all goals scored by Germany. To identify German players, check for: teamid = 'GER'
```sh
SELECT matchid, player FROM goal 
  WHERE teamid = 'GER'
```
### 2. Show id, stadium, team1, team2 for just game 1012
```sh
SELECT id,stadium,team1,team2
  FROM game
WHERE id = '1012'
```
### 3. Modify it to show the player, teamid, stadium and mdate and for every German goal.
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
### 6. List the the dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach.
```sh
SELECT mdate, teamname
FROM game JOIN eteam ON (team1=eteam.id)
WHERE coach = 'Fernando Santos'
```
### 7. List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'
```sh
SELECT player
FROM game JOIN goal ON (id=matchid)
WHERE stadium = 'National Stadium, Warsaw'
```
### 8. Show the name of all players who scored a goal against Germany.
```sh
SELECT DISTINCT player
  FROM game JOIN goal ON matchid = id 
    WHERE (team1='GER' OR team2='GER') AND teamid!= 'GER'
```
### 9. Show teamname and the total number of goals scored.
```sh
SELECT teamname, COUNT(*)
  FROM eteam JOIN goal ON id=teamid
GROUP BY teamname
```
### 10. Show the stadium and the number of goals scored in each stadium.
```sh
SELECT stadium, COUNT(*)
FROM goal JOIN game ON (matchid = id)
GROUP BY stadium
```
### 11. For every match involving 'POL', show the matchid, date and the number of goals scored.
```sh
SELECT matchid, mdate, count(*)
  FROM game JOIN goal ON matchid = id 
 WHERE (team1 = 'POL' OR team2 = 'POL')
GROUP BY matchid, mdate
```
### 12. For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'
```sh
SELECT matchid, mdate, COUNT(*)
FROM game JOIN goal ON matchid = id 
WHERE teamid = 'GER'
GROUP BY matchid, mdate
```
### 13. List every match with the goals scored by each team as shown. Sort your result by mdate, matchid, team1 and team2.
```sh
SELECT mdate,
team1,
  SUM(CASE WHEN teamid=team1 THEN 1 ELSE 0 END) AS score1,
team2,
  SUM(CASE WHEN teamid=team2 THEN 1 ELSE 0 END) AS score2
  FROM game LEFT JOIN goal ON matchid = id
  GROUP BY mdate, team1, team2
  ORDER BY mdate, matchid, team1, team2
```

No. 13 was a little bit more difficult and I had to use LEFT JOIN and CASE WHEN. CASE WHEN was used to check every time there's a goal score by a team1 and team2, we add it to the overall score of team1 or team2 of a specific game.

LEFT JOIN is used because we want to check every single matchid from 'game', and so we're checking every single game whether there is a goal or not. If we used JOIN instead of LEFT JOIN, we would only take into consideration the matches where there are goals since since the matches with no goals don't have the matchid showing up in 'goal'.
