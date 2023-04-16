# DataLemur-SQL-Solutions
Solutions to SQL Problems from Data Lemur

### 1) Second Day Confirmation [TikTok SQL Interview Question]

https://datalemur.com/questions/second-day-confirmation

SELECT user_id FROM emails LEFT JOIN texts ON

emails.email_id = texts.email_id
  
WHERE action_date = signup_date + interval '1 day'

### 2) Data Science Skills [LinkedIn SQL Interview Question]

https://datalemur.com/questions/matching-skills

SELECT candidate_id 

FROM candidates 

WHERE skill IN ('Python', 'Tableau', 'PostgreSQL')

GROUP BY candidate_id

HAVING COUNT(DISTINCT skill) = 3

ORDER BY candidate_id;

### 3) Page With No Likes [Facebook SQL Interview Question]

https://datalemur.com/questions/sql-page-with-no-likes

SELECT p.page_id 

FROM pages p

LEFT JOIN page_likes l

ON p.page_id = l.page_id

WHERE liked_date IS NULL

ORDER BY p.page_id 

### 4) Unfinished Parts [Tesla SQL Interview Question]

https://datalemur.com/questions/tesla-unfinished-parts

SELECT part , assembly_step

FROM parts_assembly 

WHERE finish_date IS NULL

### 5) Histogram of Tweets [Twitter SQL Interview Question]

https://datalemur.com/questions/sql-histogram-tweets

SELECT sq.tweet_bucket as tweet_bucket , COUNT(DISTINCT sq.user_id) AS users_num

FROM(

SELECT COUNT(DISTINCT tweet_id) AS tweet_bucket, user_id

FROM tweets 

WHERE EXTRACT('Year' FROM tweet_date) = '2022'

GROUP BY user_id)

AS sq

GROUP BY sq.tweet_bucket

### 6) 
