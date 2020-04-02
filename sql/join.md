

# JOIN  

  * 두 개 이상의 테이블에 대하여, 조건이 만족하는 경우 rows를 붙인다.  
  * **ON 조건절이 일치하는지 확인하기 위하여 N * M 비교연산 필요**  
  

## 조인의 동작  

```sql
FROM tableA
JOIN tableB
ON tableA.id = tableB.id;
```

  * tableA의 각 record에 대하여 모든 tableB의 record에 대한 비교 연산  
  
```c
table result_table;

for( record_a : tableA){                // FROM
   for( record_b : tableB){             // JOIN
      if( record_a.id = record_b.id){   // ON
          result_table.add( record_a + record_b );         
      }
   }
}
```

```sql
FROM tableA
LEFT JOIN tableB
ON tableA.id = tableB.id;
```

```c
table result_table;

for( record_a : tableA){                // FROM
   int cnt = 0;
   
   for( record_b : tableB){             // JOIN
      if( record_a.id = record_b.id){   // ON
          result_table.add( record_a + record_b );         
          cnt++;
      }
   }
   
   if(cnt == 0){
       result_bale.add( record_a + record_b filled with NULL);
   }
}
```


## 종류  

#### 1. (INNER) JOIN  
#### 2. LEFT (OUTER) JOIN  
#### 3. RIGHT (OUTER) JOIN  
#### 4. FULL (OUTER) JOIN  


## example 1 

[quetions](https://programmers.co.kr/learn/courses/30/lessons/59042)  
 
 * LEFT JOIN의 경우 ON clause에 맞추어 일치하는 rows의 합을 가져오되,  
 * RIGHT table에서 일치하는 row 가 없더라도, 그 필드를 NULL로 채워서 반환  
 
 
```sql
SELECT aout.ANIMAL_ID, aout.NAME
FROM ANIMAL_OUTS as aout
LEFT JOIN ANIMAL_INS as ain
ON aout.ANIMAL_ID = ain.ANIMAL_ID
WHERE ain.ANIMAL_ID IS NULL
```
