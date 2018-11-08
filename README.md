# Practical SQL
## - [Stanford Databases: DB5 SQL](https://lagunita.stanford.edu/courses/DB/SQL/SelfPaced/courseware/ch-sql/seq-exercise-sql_social_query_core/)
My Solution to Exercises
## - [Leetcode Database Problems](https://leetcode.com/problemset/database/)
[Solution](https://github.com/qw924/practicalSQL/tree/master/leetcode)

## - Commonly Used
- Deduplicate 
```
select * from 
table t1
    join
    (
      select id, max(date_last_modified) as max_date
      table
      group by id
    ) t2
    on (t1.id = t2.id and t1.date_last_modified = t2.max_date)
```
- Rank
```
select * from 
(select *, rank() over (partition by id order by date_last_modified desc) as rank from table) g
where rank = 1; 
```
```
select location_id, category_id, time, seller_id, category_revenue, item_cnt, revenue_share, item_share, rk
from
(select *, rank() over (PARTITION BY item_id order by market_share desc, revenue_share desc ) as rk
from item_seller_share
where location_id = ${location_id} and item_share >${item_share}
) A
WHERE rk <=${top_n};
```
- Regular Expressions
```
regexp_extract(var, 'patter') as var
```
```
regexp_extract(page_url,'.*/item/([0-9\\.]+)/',1) as item_id
```
```
regexp_extract(column, '\\;Price=([0-9\\.]+)',1) as Price
```
```
substr(TAG,1,7) = 'RECO_EXP'
```
- Time Zone
- Set Variable
```
set hivevar:this_year = 2018;
select sum(case when year(year)=${this_year} then spend else 0.0 end) as spend_this_year
```
```
set date = 20180826;
select * from table
where dt > ${hiveconf:date};
```
- [Create a Histogram](https://github.com/qw924/practicalSQL/blob/master/CreatingHistogram.md)
- Calculate a Joint Distribution
- Calculate Percentiles
## - Recommending Book: 
1. [DATABASE SYSTEM CONCEPTS](https://kakeboksen.td.org.uit.no/Database%20System%20Concepts%206th%20edition.pdf); [Slides](http://codex.cs.yale.edu/avi/db-book/db6/slide-dir/index.html)

## - Online Documentation
1. [MySQL Flow Control Statements](https://dev.mysql.com/doc/refman/5.7/en/flow-control-statements.html)
2. [SQL Tutorial - Friendly tips to help you learn SQL](http://www.wagonhq.com/sql-tutorial)
3. [Making Histogram Frequency Distributions in SQL](http://www.silota.com/docs/recipes/sql-histogram-summary-frequency-distribution.html)

## - Window Functions
1. [Postgres even included linear regressions](https://www.postgresql.org/docs/9.4/static/functions-aggregate.html)
