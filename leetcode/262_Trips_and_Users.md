## Approach I: Using case when... and where ... in ...
## Solution I
```
select Request_at as Day, 
round(sum(case when Status like "cancelled%" then 1 else 0 end)/count(*), 2) as 'Cancellation Rate'
from Trips
where Client_Id in (select Users_Id from Users where Banned = "No")
and (Request_at between "2013-10-01" and "2013-10-03")
group by Request_at
```
## Approach II: Using case when ... and join
## Solution II
```
SELECT t.Request_at Day, 
ROUND(SUM(CASE WHEN t.Status LIKE 'cancelled%' THEN 1 ELSE 0 END)/COUNT(*), 2) 'Cancellation Rate'
FROM Trips t 
JOIN Users u ON t.Client_Id = u.Users_Id AND u.Banned = 'No' 
WHERE t.Request_at BETWEEN '2013-10-01' AND '2013-10-03' 
GROUP BY t.Request_at;
```
## Approach III: Using if ... and where ... in ...
## Solution III
```
SELECT Request_at Day, 
ROUND(COUNT(IF(Status != 'completed', TRUE, NULL)) / COUNT(*), 2) 'Cancellation Rate'
FROM Trips 
WHERE (Request_at BETWEEN '2013-10-01' AND '2013-10-03') 
AND Client_Id IN
(SELECT Users_Id FROM Users WHERE Banned = 'No') 
GROUP BY Request_at;
```
## Conclusion
```
1. Use ' ' for Column name with space: 'Cancellation Rate'
2. cancelled% stands for 'cancelled_by_driver' and 'cancelled_by_client'
3. Use of Between and In (no is)
4. group by should be at the end
```
