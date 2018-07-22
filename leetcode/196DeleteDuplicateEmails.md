## Approach: Using DELETE and WHERE clause
## Solution
```
DELETE FROM Person WHERE Id NOT IN
(SELECT Id FROM (SELECT MIN(Id) Id FROM Person GROUP BY Email) p);
```
## Approach 2: Using DELETE and WHERE clause
## Solution
```
DELETE p1 FROM Person p1,
    Person p2
WHERE
    p1.Email = p2.Email AND p1.Id > p2.Id
```
## Approach 3: Using DELETE and JOIN clause
## Solution
```
DELETE p2 FROM Person p1 JOIN Person p2 
ON p2.Email = p1.Email WHERE p2.Id > p1.Id;
```
