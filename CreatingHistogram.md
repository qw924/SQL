Generating a histogram is a great way to understand that distribution. \
What’s the distribution of revenue per purchase at the banana stand? 
```
select
	revenue,
	count(*)
from banana_sales
group by revenue
order by revenue;
```
The query will specify the width of the bucket, rather than the total number.
```
select 
	floor(revenue/5.00)*5 as bucket_floor,
	count(*) as count
from banana_sales
group by 1 --group by 1st column
order by 1;
```
In order to choose our bucket size, it helps to first calculate the min/max values so we know how many buckets we would end up with. 
```
select
    bucket_floor,
    CONCAT(bucket_floor, ' to ', bucket_ceiling) as bucket_name,
    count(*) as count
from (
	select 
		floor(revenue/5.00)*5 as bucket_floor,
		floor(revenue/5.00)*5 + 5 as bucket_ceiling
	from web_sessions_table
) a
group by 1, 2 
order by 1;
```
