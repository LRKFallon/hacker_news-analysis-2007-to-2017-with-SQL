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


