
# Isolation Level  
[Ref](https://suhwan.dev/2019/06/09/transaction-isolation-level-and-lock/)  

* 트랜젝션에서의 Isolation level : **격리수준**  
* 격리수준이란 기본적으로 병렬 처리를 지원하는 DBMS에서, 동시에 여러 트랜젝션이 수행될 때  
서로가 서로에 대한 얼마나, 어느수준 정보를 참조할 수 있는지에 대한 **고립도**를 설정하는 것.  

* 고립도가 높을수록, 데이터의 **Consistency**는 증가하지만 **Trade-off**로서 **Concurrency**가 저하된다.  

### 1. 고립도  
1. read uncommitted  
2. read committed  
3. repeatble read  
4. serializable  

### 1.1. Read Uncommitted  
* 에라 모르겠다. 커밋안했고 커밋 안할 수도 있지만 읽어라.  

* 이 경우 한 트랙젝션의 변경사항을 다른 트랙젝션이 읽어들일 수 있지만  
만일 그 트랙젝션이 데이터 변경 후 commit이 아닌, **roll back**되어버리면 **Dirty Read**라는 문제가 발생.  

### 1.2. Read Committed  
* 하나의 트랜젝션의 변경사항을 **Commit된 이후 읽혀지도록 허용**하는 정도의 고립도.  

* 이는 다른 트랜젝션에서 커밋되기 이전의 값을 보다가, 커밋되면 변경된 값으로 보여지기에 **Non repeatble read**가 발생한다.  

### 1.3. Repeatable Read  
* 다른 트랜젝션의 **변경여부와 무관**하게, **일관된 데이터**를 볼 수 있는 수준의 고립도.  
* 하지만 **Phantom read**가 발생 가능.  


### 1.4. Serializable  
* 가장 엄격한 고립도를 보장한다.  
* 




















