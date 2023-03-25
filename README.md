# hacker_news-analysis-2007-to-2017-with-SQL
Using SQL to analysis the posts and contributors to ycombinator's hacker news from inception in 2007 to 2017

/* What are the top 10 sotries on Hack News between 2007 and 2017 */
SELECT title, score
FROM hacker_news
ORDER BY score DESC
LIMIT 10;

/* Considering the 1-9-90 contribution rule, how active are the top contributors? */
/* Finding the total engagement score, a measure of contribution */
SELECT SUM(score)
FROM hacker_news;

/* Finding the users that have got scores of more than 200 */
SELECT user, SUM(score)
FROM hacker_news
GROUP BY user
HAVING SUM(score) > 200
ORDER BY 2 DESC;

/* Finding the % of contribution for these users */
SELECT (517 + 309 + 304 + 282) / 6366.0;
/* Therefore, 22% of contributions are from  4 users between 2007 and 2017 */


-- Hacker News Moderating
/* Identifying and removing troll behaviour by matching spam links */
SELECT user,
   COUNT(*)
FROM hacker_news
WHERE url LIKE '%watch?v=dQw4w9WgXcQ%'
GROUP BY 1
ORDER BY 2 DESC;

-- Which sites feed hacker news?
/* Analysing three key websites that are posted to hacker news as a source */
SELECT CASE
   WHEN url LIKE '%github%' THEN 'GitHub'
   WHEN url LIKE '%medium%' THEN 'Medium'
   WHEN url LIKE '%nytimes%' THEN 'New York Times'
   ELSE 'Other website'
  END AS 'Source',
  COUNT(*)
FROM hacker_news
GROUP BY 1;

-- What is the best time to post to hacker news?
/* What is the hour of the day that will has the highest score? using SQLite's strftime() function */
SELECT strftime('%H', timestamp) AS 'Hour', 
   ROUND(AVG(score), 1) AS 'Average Score', 
   COUNT(*) AS 'Number of Stories'
FROM hacker_news
WHERE timestamp IS NOT NULL
GROUP BY 1
ORDER BY 2 DESC;

/* The best hours to post are in the morning around 7 am and afternoon around 6 - 8 pm */





