# DataLemur-SQL-Solutions
Solutions to SQL Problems from Data Lemur

1) Second Day Confirmation [TikTok SQL Interview Question]

https://datalemur.com/questions/second-day-confirmation

select user_id from emails LEFT JOIN texts ON

emails.email_id = texts.email_id
  
where action_date = signup_date + interval '1 day'
