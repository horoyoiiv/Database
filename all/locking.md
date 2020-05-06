
# Locking  

* Isolation을 보장하기 위하여 row단위, table단위 어떻게 어떤 락을 걸까?  

### 사전 지식  
1. MySQL InnoDB는 기본적으로 Repeatable Read  
2. Oracle은 Read Committed  
ANSI SQL에서는 Read uncommitted, read committed, repeatable read, serializable 네 가지로 분류.  
Oracle은 Read committed, Serializable, read-only 세 가지로 분류.  

3. SELECT ~ FOR SHARE  
* 이 구문은 해당 (row, table)? 에 대한 exclusive lock을 명시적으로 거는 방법.  

### InnoDB 기준  
#### [Lock's](https://suhwan.dev/2019/06/09/transaction-isolation-level-and-lock/)  

1. Row Lock  
table의 행단위로 걸게 되는 락  
* S Lock  
* X Lock  

2. Record Lock  
* Index에 걸리는 락.  

3. Gap Lock  
* Index의 **빈 부분**에 걸리는 락  
* 비록 아직 레코드가 없지만, 그 부분에 락을 걸어 새로운 값의 추가를 막는다.  


### Lock이 해제되는 타이밍.  
* Commit 혹은 Rollback될 때, Lock들은 해제된다.  








