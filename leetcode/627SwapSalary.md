## Approach One: Using UPDATE and CASE...WHEN
## Solution One
```
UPDATE salary
SET
    sex = CASE sex WHEN 'm' THEN 'f' ELSE 'm' END
    ;
```

```
Update salary
set 
    sex = case when sex = 'm' then 'f' else 'm' end
    ;
```
## Approach Two: Using UPDATE and IF
## Solution Two
```
UPDATE salary
SET sex = IF(sex='f','m','f');
```
