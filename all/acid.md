

# ACID  
* ACID 는 트랙젝션이 만족해야 할 속성을 의미한다.  


#### 1. Atomicity  
* **원자성**  

트랜젝션이 **여러 statement로 구성**될 경우 이 중 일부만 실행되는 것이 아닌, **전부 실행되거나 아니면 아싸리 전부 실행하지 않아**야 하는 **All or Nothing** 속성.  


#### 2. Consistency  
* **일관성**  

* 데이터베이스에는 그것에 **고유한 rule**이 있다.  
* 이들 rule에는 **Domain Integrity**, **Primary key Integrity**, **Referential Integrity** 등을 포함한 **무결성 제약 조건**이다.  
```sql
// ENUM을 통한 도메인 인테그리티 제약조건 
CREATE TABLE user (
    name VARCHAR(40),
    sex ENUM('male', 'female')
);
```
* 트랜젝션 전과 후에는 DB의 상태는 변할 수 있지만, 일관성은 유지되는 상태를 보장해야 하는 것이 Consistency.  


#### 3. Isolation  
* 고립도  
* 실행 중인 하나의 트랜젝션은 **다른 트랙젝션에서 수행된 연산**에 **영향을 받으면 안된다**는 속성.  
* 하지만 이러한 Isolation 속성을 지킨다면 **Concurrency**가 저하되기에, Isolation level을 설정하여 Trade-off를 결정해야 할 것.  


#### 4. Durability  
* 지속성  
* Commit된 트랜젝션의 결과는 **하드웨어적** 혹은 **소프트웨어적** 장애가 발생하더라도 영구히 반영되어야 한다는 속성.  












