

# SQL 실행 순서  

```sql
SELECT *, AVG(field) 
FROM table a
JOIN table b
ON criteria
WHERE criteria
GROUP BY field
HAVING criteria
ORDER BY AVG(field)
LIMIT a OFFSET b
```

1. FROM을 통해서 LEFT table을 조회.  
2. JOIN에 주어진 RIGHT table을 ON절의 조건에 맞춘 임시 테이블 생성  
3. WHERE 문에서 해당 조건에 일치하는 레코드만 선택  
4. GROUP BY를 통해 주어진 필드를 기준으로 레코드를 그룹화  
5. HAVING을 통해 그룹화 된 레코드에 대한 criteria를 적용  
6. ORDER BY를 통해 정렬  
7. LIMIT과 OFFSET이 주어진다면 그 크기만큼 페이지네이션 수행.  
8. SELECT 절에 명시된 필드를 기준으로 프로젝션 수행 후 결과 반환.  










