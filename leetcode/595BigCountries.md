## Approach One: Using WHERE clause and OR
## Solution for Approach One
```
SELECT
    name, population, area
FROM
    world
WHERE
    area > 3000000 OR population > 25000000
;
```
## Approach Two: Using WHERE clause and UNION
## Solution for Approach Two
```
SELECT
    name, population, area
FROM
    world
WHERE
    area > 3000000

UNION

SELECT
    name, population, area
FROM
    world
WHERE
    population > 25000000
;
```
## Conclusion: Solution Two runs faster than Solution One.
