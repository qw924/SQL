## Approach: Using <>(!=) and IS NULL
```
SELECT name FROM customer WHERE referee_id <> 2 OR referee_id IS NULL;
```
or
```
SELECT name FROM customer WHERE referee_id != 2 OR referee_id IS NULL;
```
