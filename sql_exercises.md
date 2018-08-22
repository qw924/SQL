## Question 1
For each user_id, find the difference between the last action and the second last action. Action
here is defined as visiting a page. If the user has just one action, you can either remove her from
the final results or keep that user_id and have NULL as time difference between the two actions.
The table below shows for each user all the pages she visited and the corresponding
timestamp.

### head (query_one,1)
Column Name | Value | Description\
user_id | 6684 | this is id of the user\
page | home_page | the page visited\
unix_timestamp | 1451640067 | unix timestamp in seconds\

```
select user_id, unix_timestamp - previous_time as delta_secondlast_last
from 
(select user_id, unix_timestamp, lag(unix_timestamp, 1) over (partition by user_id order by unix_timestamp) as previous_time,
row_number() over (partition by user_id order by unix_timestamp) as order_desc
from table) tmp 
where order_desc = 1
order by user_id;
```

## Question 2
We have two tables. One table has all mobile actions, i.e. all pages visited by the users on
mobile. The other table has all web actions, i.e. all pages visited on web by the users.
Write a query that returns the percentage of users who only visited mobile, only web and both.
That is, the percentage of users who are only in the mobile table, only in the web table and in
both tables. The sum of the percentages should return 1.

### head (data_mobile,1)
Column Name | Value | Description\
user_id | 128 | this is id of the user who visited a given page on mobile\
page | page_5_mobile | page visited by that user on mobile

### head (data_web,1)
Column Name | Value | Description\
user_id | 1210 | this is id of the user who visited a given page on web\
page | page_1_web | page visited by that user on web

```
select 100*sum(case when m.user_id is null then 1 else 0 end)/count(*) as web_only,
100*sum(case when w.user_id is null then 1 else 0 end)/count(*) as mobile_only,
100*sum(case when m.user_id is not null and w.user_id is not null then 1 else 0 end)/count(*) as both
from 
(SELECT distinct user_id FROM web ) w
FULL OUTER JOIN
(SELECT distinct user_id FROM mobile ) m
ON m.user_id = w.user_id;
```
## Question 3
We define as power users those users who bought at least 10 products. Write a query that
returns for each user on which day they became a power user. That is, for each user, on which
day they bought the 10th item.
The table below represents transactions. That is, each row means that the corresponding user
has bought something on that date.

### head (data,1)
Column Name | Value | Description
user_id | 675 | this is id of the user
date | 2014-12-31 16:16:12 | user 675 bought something on Dec 31, 2014 at 4:16:12 PM
```
select user_id, date 
from 
(select user_id, data, row_number() over (partition by user_id order by date) as row_num from data) tmp
where row_num = 10;
```
## Question 4
We have two tables. One table has all $ transactions from users during the month of March and
one for the month of April.
1. Write a query that returns the total amount of money spent by each user. That is, the sum
of the column transaction_amount for each user over both tables.\
2. Write a query that returns day by day the cumulative sum of money spent by each user.
That is, each day a user had a transcation, we should have how much money she has
spent in total until that day. Obviously, the last day cumulative sum should match the
numbers from the previous bullet point.

### head (data_march,1)
Column Name | Value | Description\
user_id | 13399 | this is id of the user who had the corresponding transaction\
date | 2015-03-01 | the transaction happened on March 1st.\
transaction_amount | 18 | the user spent 18$ in that transaction
### head (data_april,1)
Column Name | Value | Description\
user_id | 15895 | this is id of the user who had the corresponding transaction\
date | 2015-04-01 | the transaction happened on April 1st.\
transaction_amount | 66 | the user spent 66$ in that transaction

```
SELECT user_id,
SUM(transaction_amount) as total_amount
FROM
(
SELECT * FROM data_march
UNION ALL
SELECT * FROM data_april
) tmp
GROUP BY user_id;
```

```
SELECT user_id, date,
SUM(amount) over(PARTITION BY user_id ORDER BY date) as total_amount
FROM
(
SELECT user_id, date, SUM(transaction_amount) as amount
FROM data_march
GROUP BY user_id, date
UNION ALL
SELECT user_id, date, SUM(transaction_amount) as amount
FROM data_april
GROUP BY user_id, date
) tmp
ORDER BY user_id, date;
```

