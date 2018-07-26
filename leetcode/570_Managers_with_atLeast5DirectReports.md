## Approach I: Using JOIN and a temporary table
```
SELECT
    Name
FROM
    Employee AS t1 JOIN
    (SELECT
        ManagerId
    FROM
        Employee
    GROUP BY ManagerId
    HAVING COUNT(ManagerId) >= 5) AS t2
    ON t1.Id = t2.ManagerId
;
```
## Approach II: Using In and a temporary table
```
Select 
    Name
from 
    Employee
where Id in 
    (select ManagerId
     from Employee
     group by ManagerId
     having count(Id) >= 5) 
```
## Conclusion: Approach II is faster than Approach I.
