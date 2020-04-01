


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
