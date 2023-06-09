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

#Method 1

SELECT p.page_id 

FROM pages p

LEFT JOIN page_likes l

ON p.page_id = l.page_id

WHERE liked_date IS NULL

ORDER BY p.page_id 

#Method 2

SELECT page_id

FROM pages

WHERE page_id NOT IN (

  SELECT page_id 
  
  FROM page_likes
  
  )
 
 ORDER BY page_id

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

#Method1

WITH cte AS


(SELECT company_id, title, description, count(*)

FROM job_listings

GROUP BY company_id, title, description

HAVING count(*) > 1)

SELECT COUNT(*) 

FROM cte

#Method2

SELECT COUNT(*)

FROM(

SELECT company_id

FROM job_listings 

GROUP BY company_id , title , description

HAVING COUNT(*) > 1

) AS sq

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

### 11) Average Review Ratings [Amazon SQL Interview Question]

https://datalemur.com/questions/sql-avg-review-ratings

SELECT EXTRACT('Month' FROM submit_date) AS mth , product_id as product , ROUND(AVG(stars),2) as avg_stars

FROM reviews 

GROUP BY product_id,  EXTRACT('Month' FROM submit_date)

ORDER BY mth , product_id

### 12) Final Account Balance [Paypal SQL Interview Question]

https://datalemur.com/questions/final-account-balance

SELECT account_id , 

  SUM(CASE 
  
       WHEN transaction_type = 'Deposit' THEN (amount)
       
       WHEN transaction_type = 'Withdrawal' THEN (-amount)
       
      END) AS final_balance


FROM transactions 

GROUP BY account_id

### 13) QuickBooks vs TurboTax [Intuit SQL Interview Question]

https://datalemur.com/questions/quickbooks-vs-turbotax

WITH T AS (

  SELECT COUNT(filing_id) AS turbotax_total
  
  FROM filed_taxes 
  
  WHERE product LIKE '%TurboTax%' ),
  
 Q AS (

  SELECT COUNT(filing_id) AS quickbooks_total
  
  FROM filed_taxes 
  
  WHERE product LIKE '%QuickBooks%'

)

SELECT * FROM T, Q

### 14) App Click-through Rate (CTR) [Facebook SQL Interview Question]

https://datalemur.com/questions/click-through-rate

WITH Click AS  (

SELECT app_id, COUNT(event_type) AS c

FROM events 

WHERE event_type LIKE 'click' AND EXTRACT('Year' FROM timestamp) = '2022'

GROUP BY app_id) ,

 imp AS ( 

SELECT app_id, COUNT(event_type) AS i

FROM events 

WHERE event_type LIKE 'impression' AND EXTRACT('Year' FROM timestamp) = '2022'

GROUP BY app_id)

SELECT imp.app_id , ROUND( 100.0* click.c / imp.i  , 2) AS ctr

FROM click 

INNER JOIN imp

ON click.app_id = imp.app_id

### 15) Cards Issued Difference [JPMorgan Chase SQL Interview Question]

https://datalemur.com/questions/cards-issued-difference

SELECT card_name	, MAX(issued_amount) - MIN(issued_amount) AS difference

FROM monthly_cards_issued 

GROUP BY card_name

ORDER BY difference DESC

### 16) Compressed Mean [Alibaba SQL Interview Question]

https://datalemur.com/questions/alibaba-compressed-mean

#Method1

SELECT ROUND( 1.0 * SUM(item_count*order_occurrences) / SUM(order_occurrences) ,1) AS mean
 
FROM items_per_order ;

#Method2 - Using CAST() : Change type to decimal for rounding , changing it to float will give an error

SELECT 

   ROUND(CAST(SUM(item_count*order_occurrences) AS decimal ) /  CAST(SUM(order_occurrences) AS decimal ) , 1) 
        
 as mean

FROM items_per_order 

### 17) Patient Support Analysis (Part 1) [UnitedHealth SQL Interview Question]

https://datalemur.com/questions/frequent-callers

SELECT COUNT(sq.policy_holder_id) AS member_count

FROM(

SELECT policy_holder_id 

FROM callers

GROUP BY policy_holder_id 

HAVING COUNT(case_id) >= 3 ) AS sq

### 18) Patient Support Analysis (Part 2) [UnitedHealth SQL Interview Question]

https://datalemur.com/questions/uncategorized-calls-percentage

SELECT  ROUND((100.0 * COUNT( * )) / (SELECT COUNT( * ) FROM callers),1) AS call_percentage

FROM callers

WHERE call_category IS NULL OR call_category LIKE 'n/a' 

### 19) User's Third Transaction [Uber SQL Interview Question]

https://datalemur.com/questions/sql-third-transaction

SELECT sq.user_id , sq.spend , sq.transaction_date 

FROM

(SELECT * , ROW_NUMBER() OVER(PARTITION BY user_id ORDER BY transaction_date ASC) as rn

FROM transactions ) AS sq

WHERE rn = 3

### 20) Sending vs. Opening Snaps [Snapchat SQL Interview Question]

https://datalemur.com/questions/time-spent-snaps

WITH cte AS 

  (SELECT ag.age_bucket as age_bucket,
       SUM(CASE WHEN activity_type='open' THEN time_spent ELSE 0 END) AS open,
       SUM(CASE WHEN activity_type='send' THEN time_spent ELSE 0 END) AS send,
       SUM(CASE WHEN activity_type IN ('open','send') THEN time_spent ELSE 0 END) AS open_send
FROM activities ac   
LEFT JOIN age_breakdown ag    
ON ac.user_id = ag.user_id
GROUP BY ag.age_bucket )

SELECT age_bucket,
       ROUND((100.0 * send/open_send),2) AS send_perc,
       ROUND((100.0 * open/open_send),2) AS open_perc
FROM cte


###21)


          






