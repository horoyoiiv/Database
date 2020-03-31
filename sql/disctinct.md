

# DISTINCT  
  * Remove the duplicates.  
  
## 1) 칼럼의 범주 조회  

```sql
SELECT DISTINCT column FROM table; 
```

## 2) 조건 처리 후 칼럼 범주 조회.  

```sql
SELECT DISTINCT column FROM table WHERE ~; 
```

## 3) 칼럼의 범주의 개수 조회  

```sql
SELECT COUNT(DISTINCT column) FROM table;  
```

[Example](https://programmers.co.kr/learn/courses/30/lessons/59408)  

```sql
SELECT COUNT(DISTINCT NAME) FROM ANIMAL_INS;
```




