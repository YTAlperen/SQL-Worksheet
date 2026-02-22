# SQL-Worksheet

SQL Case Statement 1.1 Likes
```
SELECT actor, character, platform, avg_likes, 
case 
  when avg_likes >= 15000 then 'Super Likes'
  when avg_likes between 5000 and 14999 then 'Good Likes'
  else 'Low Likes'
end as likes
FROM marvel_avengers
order by avg_likes DESC;
```

SQL Case Statement 1.2 Laptop vs. Mobile Viewership
```
SELECT 
sum(case 
      when device_type = 'laptop' then 1
      else 0
end) as laptop_views,
sum(case
      when device_type = 'phone' or device_type = 'tablet' then 1
      else 0
end) as mobile_views
FROM viewership;
```

---------------------------------

SQL Joins 1.1 Easy SQL JOIN Practice Exercise
```
SELECT * FROM trades
join users on trades.user_id = users.user_id;
```

SQL Joins 1.2 Cities With Completed Trades
```
SELECT users.city, count(order_id) as total_orders FROM trades
join users on trades.user_id = users.user_id
where trades.status = 'Completed'
group by users.city
order by count(order_id) DESC
limit 3;

```

SQL Joins 1.3 Page With No Likes
```
SELECT pages.page_id FROM pages
LEFT OUTER join page_likes
  on pages.page_id = page_likes.page_id
where page_likes.page_id is null
order by pages.page_id ASC;
```

--------------------------------------


Date Functions 1.1 Average Post Hiatus (Part 1)
```
SELECT user_id, 
extract(DAY from max(post_date) - min(post_date)) as days_between
FROM posts
where 
  date_part('year', post_date::date)=2021
group by user_id
HAVING 
  count(post_id)>1;
```

Date Functions 1.2 Second Day Confirmation
```
SELECT user_id FROM emails
join texts
  on emails.email_id = texts.email_id
where texts.signup_action = 'Confirmed'
and extract(day from texts.action_date)-extract(day from emails.signup_date) = 1;
```
