what are the 25th, 50th, 75th percentiles of wait-time, and how does that number vary day to day?
```
SELECT
	date,
	percentile_cont (0.25) WITHIN GROUP
		(ORDER BY wait_time ASC) OVER(PARTITION BY date) as percentile_25,
	percentile_cont (0.50) WITHIN GROUP
		(ORDER BY wait_time ASC) OVER(PARTITION BY date) as percentile_50,
	percentile_cont (0.75) WITHIN GROUP
		(ORDER BY wait_time ASC) OVER(PARTITION BY date) as percentile_75,
	avg(wait_time) as avg -- for comparison
FROM banana_sales
GROUP BY date
ORDER BY date;
```
Calculate Median by date
```
SELECT
	t1.date,
	t1.wait_time as median
FROM (	
	SELECT
		date,
		wait_time,
		ROW_NUMBER() OVER(ORDER BY wait_time PARTITION BY date) as row_num
	FROM banana_sales
) t
JOIN (
	SELECT
		date,
		count(*) as total
	FROM banana_sales
	GROUP BY date
) t2
	ON
		t1.date = t2.date
-- for simplicity, we take a simple solution when the list has an even length, to just choose one value
WHERE t1.row_num =
  CASE when t2.total % 2 = 0 
		THEN t2.total / 2
		ELSE (t2.total + 1) / 2
	END;
  ```
