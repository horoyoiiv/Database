# Database

## Index  
### [1. Index](/all/index.md)  
* 1.SELECT 성능을 향상시키기 위한 추가적인 자료구조. 
* 2. 대게 (하나의 노드가 하나의 페이지 크기에 매핑될 수 있는) B-tree를 사용하여 구현  
* 3.1. SELECT / JOIN 등의 연산은 로그 타임이 되지만, 3.2. 삽입 등 연산에 대해서는 더 느려짐.
* 4. 그렇기에 where절이나 on절에 자주 사용되지만, 변화는 많이 발생안하는 필드에 적용.  
* 5. 하지만 실제로 적용 후 성능 측정을 해보고, 향상된 성능이 trade-off만큼의 가치가 있었는지 판단.  


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
