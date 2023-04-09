# DataLemur-SQL-Solutions
Solutions to SQL Problems from Data Lemur

1) Second Day Confirmation [TikTok SQL Interview Question]

https://datalemur.com/questions/second-day-confirmation

SELECT user_id FROM emails LEFT JOIN texts ON

emails.email_id = texts.email_id
  
WHERE action_date = signup_date + interval '1 day'
