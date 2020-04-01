

# GROUP BY  

  * 주로 Aggregate 함수 - COUNT, MAX, MIN, SUM, AVG 와 함께 쓰인다.  
  
```sql
GROUP BY column명 (Coutnry)  
```
  * GROUP BY를 통해 지정된 **column**에 대하여 **동일한 value**끼리 묶는다.  
  

## WHAT?  

```sql
SELECT ANIMAL_TYPE 
FROM ANIMAL_INS;
```
위의 쿼리 결과 모든 타입을 중복되게 결과를 가져옴.  

```
dog
dog
dog
cat
cat
```

아래와 같이 **DISTINCT**를 통해 중복이 제거된 값만을 가져올 수 있음.  
```sql
SELECT DISTINCT ANIMAL_TYPE 
FROM ANIMAL_INS;
```

```
dog
cat
```

 * **GROUP BY**를 통해서도 위와 같이 고유한 value를 조회할 수 있다.  
 
 ```sql
 SELECT ANIMAL_TYPE
 FROM ANIMAL_INS
 GROUP BY ANIMAL_TYPE;
 ```
 
 ```
 dog
 cat
 ```

#### 중요한 차이점은 GROUP BY는 aggregate 함수를 통해 column의 통계정보를 확인할 수 있음.  

```sql
 SELECT ANIMAL_TYPE
 FROM ANIMAL_INS
 GROUP BY ANIMAL_TYPE;
```

```sql
 SELECT ANIMAL_TYPE, COUNT(*)
 FROM ANIMAL_INS
 GROUP BY ANIMAL_TYPE;
```

* 각 그룹에 대한 통계정보(aggregate 결과)를 찾을 수 있다.  
```
dog  3
cat  2
```
  
#### 남자가 몇명이고, 여자가 몇명인지 등의 정보를 찾기위해 사용가능.  


  
## HAVING  
  * WHERE과의 차이가 있다.  
  * HAVING은 GROUP BY 후의 결과 그룹에 대한 조건을 거는 것.  
  
  * **WHERE은 그룹화 전에 적용되는 조건문이고, HAVING은 그룹화 후에 적용되는 조건문**  
  


## Example  
  
  * 모든 테이블의 row에 대하여 where을 만족하는 rows를 가져온 후  
  * 그룹화를 수행하고  
  * 그 그룹에 대한 HAVING 조건을 만족하는 결과를 리턴  
```sql
SELECT *
FROM table
WHERE 조건1
GROUP BY column
HAVING 조건2
```


## Example 2  

  * NULL을 집계에서 제외하며, 동물 이름 중 두번 이상 쓰인 이름에 대하여 그 이름과 그 횟수를 반환.  

```sql
SELECT NAME, COUNT(*)
FROM ANIMAL_INS
WHERE NAME IS NOT NULL
GROUP BY NAME
HAVING COUNT(*) >=2;
```
  
## Example 3  

  * datatime에 대하여 **9시 이후 19시 이전**의 입양 **시간**의 빈도 계산  
  
```sql
SELECT HOUR(DATETIME) AS HOUR, COUNT(DATETIME)
FROM ANIMAL_INS
WHERE HOUR(DATETIME) >=9 AND HOUR(DATETIME) <= 19
GROUP BY HOUR(DATETIME)
ORDER BY HOUR(DATETIME);
```


```
