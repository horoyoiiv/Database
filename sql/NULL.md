


## 1. COUNT  

  * 특정 필드 명시하게 되면 **NULL을 제외**하고 갯수를 반환.  
```sql
SELECT COUNT(NAME)
FROM ANIMAL_INS;
```

```
99
```

```sql
SELECT COUNT(*)
FROM ANIMAL_INS;
```

```
100
```


## IS NULL  

  * 이름이 없는 채로 들어온 동물의 수  
  
```sql
SELECT COUNT(*)
FROM ANIMAL_INS
WHERE NAME IS NULl
```


## IS NOT NULL  
  * 이름이 있는 동물의 아이디  
  
```sql
SELECT COUNT(*)
FROM ANIMAL_INS
WHERE NAME IS NOT NULL
```

## IFNULL(컬럼명, '디폴트값')  
  * 특정 column이 null인 경우 '디폴트값'으로 대체하여 출력  
  
```sql
SELECT AGE, IFNULL(NAME, 'this is null'), LOCATION
FROM ANIMAL_INS;
```



