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

### 6) Laptop vs. Mobile Viewership [New York Times SQL Interview Question]

https://datalemur.com/questions/laptop-mobile-viewership

WITH l_cte AS (

SELECT COUNT(user_id)  AS lv

FROM viewership 

WHERE device_type = 'laptop' 

),

m_cte AS (

SELECT (COUNT(*))  AS mv

FROM viewership 

WHERE device_type = 'tablet' OR device_type = 'phone'

)

SELECT l_cte.lv AS laptop_views,  m_cte.mv AS mobile_views

### 7) Duplicate Job Listings [Linkedin SQL Interview Question]

https://datalemur.com/questions/duplicate-job-listings

WITH cte AS


(SELECT company_id, title, description, count(*)

FROM job_listings

GROUP BY company_id, title, description

HAVING count(*) > 1)

SELECT COUNT(*) 

FROM cte

### 8) Average Post Hiatus (Part 1) [Facebook SQL Interview Question]

https://datalemur.com/questions/sql-average-post-hiatus-1

SELECT sq.user_id , sq.days_between 

FROM(

SELECT user_id , EXTRACT('Days' FROM MAX(post_date) - MIN(post_date)) AS days_between

FROM posts 

WHERE EXTRACT('Year' FROM post_date) = '2021' 

GROUP BY user_id ) AS sq

WHERE sq.days_between > 0 

### 9) Teams Power Users [Microsoft SQL Interview Question]

https://datalemur.com/questions/teams-power-users

SELECT sender_id , COUNT(*) AS message_count

FROM messages 

WHERE EXTRACT('Month' FROM sent_date) = '8' AND EXTRACT('Year' FROM sent_date) = '2022'

GROUP BY sender_id

ORDER BY message_count DESC

LIMIT 2

### 10) Cities With Completed Trades [Robinhood SQL Interview Question]

https://datalemur.com/questions/completed-trades

SELECT u.city  , COUNT(t.status) as total_orders

FROM users u 

RIGHT JOIN trades t  

ON u.user_id = t.user_id

WHERE t.status = 'Completed'

GROUP BY u.city

ORDER BY total_orders DESC

LIMIT 3

### 11) 
