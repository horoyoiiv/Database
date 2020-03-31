  
  
# LIKE  
 
 * This operator is used in **WHERE** clause to search for a **specified pattern** in a column.  
 
 
## Two wildcard  
 
 #### 1) % : 0, 1, 그 이상  
 #### 2) _ : 하나의 문자  
 
[Examples](https://www.w3schools.com/sql/sql_like.asp)  
  
 
## Examples  
 
 * Finds any values that start with "a"  
 ```sql
 select * 
 from products
 where name LIKE 'a%'
 ```
 
 * Finds any values that end with "a"  
 ```sql
  select * 
 from products
 where name LIKE '%a'
 ```
 
 * Finds any values that have "and" in any position  
 ```sql
select * 
from products
where name LIKE '%and%'
 ```
 
 * Finds any values that have "r" in the second position  
 ```sql
select * 
from products
where name LIKE '_a%'

```
 * Finds any values that start with "a" and are at least 2 characters in length   
 
 ```sql
select * 
from products
where name LIKE 'a__%'

```
 
 * Finds any values that start with "a" and ends with "o"  
 ```sql
select * 
from products
where name LIKE 'a%o'

```
 
