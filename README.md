# SQL-Worksheet

Date Function 1.1
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
