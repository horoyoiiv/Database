# Database



## Transaction  
* 데이터베이스에서 수행되는 작업의 단위.  

###### 트랙젝션은 아래의 ACID 속성을 만족해야 한다.
### [1. ACID](/all/acid.md)  

###### 하지만 Isolation의 추구는 성능저하를 유발하기에, Isolation level을 조정하여 Trade-off의 강도를 조율한다.  
### [2. Isolation level](/all/isolation.md)  

## Recovery  
* [Naver D2](https://d2.naver.com/helloworld/407507)  
#### [1. 복구 전략](/all/recovery.md)  
버퍼 캐시 정책인 **STEAL**과 **NO-FORCE**를 바탕으로 이어지는 **UNDO**와 **REDO** 로그를 바탕으로 수행.  


## SQL statements  

[1. select](/sql/select.md)  
  This is about  
  * ORDER BY / LIMIT / WHERE  
 
 
[2. min/max/sum/count/avg](/sql/min-max-sum.md)  
   
  
[3. DISTINCT](/sql/disctinct.md)  
   * SELECT COUNT( DISTINCT NAME ) FROM table;  
   

[4. LIKE](/sql/LIKE.md)  
This is for pattern matching.  
