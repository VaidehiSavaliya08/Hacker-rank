# Hacker-rank
SQL

You are given a table, BST, containing two columns: N and P, where N represents the value of a node in Binary Tree, and P is the parent of N.



Write a query to find the node type of Binary Tree ordered by the value of the node. Output one of the following for each node:

Root: If node is root node.
Leaf: If node is leaf node.
Inner: If node is neither root nor leaf node.



SELECT n, CASE
WHEN p is null THEN 'Root'
WHEN n IN (SELECT p FROM bst)  THEN 'Inner'
ELSE 'Leaf'
END FROM bst ORDER BY n


1.Average Population of Each ContinentGiven the CITY and COUNTRY tables, query the names of all the continents (COUNTRY.Continent) and their respective average city populations (CITY.Population) rounded down to the nearest integer.

Note: CITY.CountryCode and COUNTRY.Code are matching key columns.


SELECT country.continent, FLOOR(AVG(city.population))
FROM country  city 
WHERE country.code = city.countryCode 
GROUP BY country.continent;

OR

SELECT country.continent, FLOOR(AVG(city.population))
FROM country  INNER JOIN city ON country.code = city.countryCode 
GROUP BY country.continent ;


2.Top Competitors

Julia just finished conducting a coding contest, and she needs your help assembling the leaderboard! Write a query to print the respective hacker_id and name of hackers who achieved full scores for more than one challenge. Order your output in descending order by the total number of challenges in which the hacker earned a full score. If more than one hacker received full scores in same number of challenges, then sort them by ascending hacker_id.



SELECT h.hacker_id ,h.name 
FROM hackers  h 
JOIN submissions s ON s.hacker_id = h.hacker_id 
JOIN challenges c ON c.challenge_id = s.challenge_id 
JOIN difficulty d ON d.difficulty_level = c.difficulty_level AND 
d.score = s.score 
GROUP BY h.hacker_id , h.name 
HAVING COUNT(s.challenge_id) > 1
ORDER BY COUNT(s.score) DESC ,s.hacker_id;


