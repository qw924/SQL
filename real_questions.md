```
select a.name, round(avg(a.comments),2)
    from comments a
    inner join
    
    -- get users who has more than two posts and each posts with more than 40 comments
    (select name, count(distinct posts) as numb from comments
        where comments >= 40
        group by name
        having numb >=2) b
   
    on a.name = b.name
    group by a.name;
```
