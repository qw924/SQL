## Approach: Using MOD() function
use the mod(id,2)=1 to determine the odd id
```
select *
from cinema
where mod(id, 2) = 1 and description != 'boring'
order by rating DESC
;
```
