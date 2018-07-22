## Approach I: Using GROUP BY and a temporary table
## Solution I
```
select Email from
(
  select Email, count(Email) as num
  from Person
  group by Email
) as statistic
where num > 1
;
```

## Approach II: Using GROUP BY and HAVING condition [Accepted]
## Solution II
```
select Email
from Person
group by Email
having count(Email) > 1;
```
```
select Email
from Person
group by Email
having count(*) > 1
```
