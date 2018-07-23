## Approach I: Using JOIN and DATEDIFF() clause
## Solution I
```
SELECT
    weather.id AS 'Id'
FROM
    weather
        JOIN
    weather w ON DATEDIFF(weather.date, w.date) = 1
        AND weather.Temperature > w.Temperature
;
```

## Approach II: Using Where and TO_Days() clause
## Solution II
```
select w1.Id 
from Weather w1, Weather w2 
where w1.Temperature>w2.Temperature 
and TO_DAYS(w1.RecordDate)-TO_DAYS(w2.RecordDate)=1
```

## Conclusion
1. a.date = b.date + 1 doesn't work becuase of special cases (the end of this month and the begin of next month).
2. Solution I is faster than Solution II.
