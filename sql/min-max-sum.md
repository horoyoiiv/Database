

# MAX(Column)  
  * Retrieve the maximum value of the column.  
  
```sql
SELECT MAX(Price)
FROM Products
```

  * Also this value can be retrieved by the below sql using ORDER BY and LIMIT.  
  
```sql
SELECT Price 
FROM Products
ORDER BY Price DESC
LIMIT 1;
```

# MIN(Column)  
 * Retrieve the minimum value of the column.  
 
```sql
SELECT MIN(Price) as smallest_value
FROM Products;
 ```
 
# SUM(Column)  
  * Retrieve the sum of the specific column.  
  

```sql
SELECT SUM(Price)
FROM Products;
```
 
# COUNT(*) or COUNT(column)  
  * Retrieve the count of the column.  
  
```sql
SELECT COUNT(*)
FROM Products;
```

  * 1000원 이상인 물품의 개수  
```sql
SELECT COUNT(*)
FROM Products
WHERE Price >= 1000;
```


# AVG(column)  
  * Retrieve the avg of the column.  
  
```sql
SELECT AVG(Price)
FROM Products;
```

