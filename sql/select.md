[Ref](https://ko.khanacademy.org/computer-programming/sql-select-with-order-by/6218182226477056)  
  
  
# Select  

## Sequence  

```
5. SELECT 칼럼명  [ALIAS명]   
1. FROM 테이블명   
2. WHERE 조건식   
3. GROUP BY 칼럼(Column)이나 표현식   
4. HAVING 그룹조건식   
6. ORDER BY 칼럼(Column)이나 표현식;
```

1. 발췌 대상 테이블을 참조한다. (FROM)
2. 발췌 대상 데이터가 아닌 것은 제거한다. (WHERE)
3. 행들을 소그룹화 한다. (GROUP BY)
4. 그룹핑된 값의 조건에 맞는 것만을 출력한다. (HAVING)
5. 데이터 값을 출력/계산한다. (SELECT)
6. 데이터를 정렬한다. (ORDER BY)


## ORDER BY  
  * If you just use the SELECT clause, the rows get returend in the same order they are inserted.  
  * By adding **ORDER BY**, you can change the order.  
  * By default, the ordering will be **ascending order**.  
  * To get a descending order, **ORDER BY colum DESC**.  
  

```sql
SELECT * FROM skyscrapers ORDER BY height_meters;
```

```sql
SELECT * FROM skyscrapers ORDER BY height_meters DESC;
```

#### Two ORDER BY  
```
 이름이 같은 동물 중에서는 보호를 나중에 시작한 동물을 먼저 보여줘야 합니다.
```
[Quetion](https://programmers.co.kr/learn/courses/30/lessons/59404)  

```sql
SELECT t1.ANIMAL_ID, t1.NAME, t1.DATETIME
FROM ANIMAL_INS AS t1
ORDER BY t1.NAME, t1.DATETIME DESC;
```

 * If there are more than one parameter after the ORDERB BY clause,  
 First, the rows get ordered in ascending order by NAME.  
 But when names are same, then comparision based on DATETIME is applied.   



## RENAME  
  * To change the field name, you can use **AS** keyword.  
  

```sql
SELECT t1.tb_name AS name, t1.tb_date AS data
FROM table AS t1
ORDER BY t1.id;
```
 
## WHERE  
  * WHERE name = "hello"  
  * WHERE name = 'hello'  
  both are fine.  
  
  
```sql
SELECT t1.ANIMAL_ID, t1.NAME
FROM ANIMAL_INS AS t1
WHERE t1.INTAKE_CONDITION = "Sick";
```


```sql
SELECT t1.ANIMAL_ID, t1.NAME
FROM ANIMAL_INS AS t1
WHERE t1.INTAKE_CONDITION != "Sick";
```
  


## LIMIT  
  * Only gets some columns.  
  
  * **Only shows top 10 rows after ORDER BY**  
```sql
SELECT NAME 
FROM ANIMAL_INS
ORDER BY DATETIME
LIMIT 10;
```

  * **LIMIT OFFSET, NUMBER**  
  * **From index 0 rows, get 5 rows.   
```sql
SELECT NAME 
FROM ANIMAL_INS
ORDER BY DATETIME
LIMIT 0, 5;
```

  * After that, we can continously serve the next five rows.  
```sql
SELECT NAME 
FROM ANIMAL_INS
ORDER BY DATETIME
LIMIT 5, 5;
```





