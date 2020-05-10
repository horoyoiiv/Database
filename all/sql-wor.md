
# SQL 동작 과정  
## [SQL how it works](https://hayleyfish.tistory.com/65)  
## [how it works](https://o2sunn.tistory.com/4)  

## 1. Parsing  

* DBMS에 주어진 사용자의 **SQL** 구문을 파싱한다.  

#### 1.1. syntax 검사  
* sql 문법에 대한 검사  
#### 1.2. semantic 검사  
* 요청한 테이블 혹은 필드에 대한 이름이 유효한가  
#### 1.3. shared pool 검사  
* 요청한 사용자의 권한 확인  

#### 1.4. parsing tree 생성  


## 2. Optimization  
#### [Good](http://bysql.net/w201102TA/17855)  

### 2.1 Query Transformer  
* 쿼리를 표준적인 형태로 변화하여 **Estimator**에게 넘겨준다.  

### 2.2. Estimator  
* **Selectivity** : 전체 레코드 대비, 해당 쿼리로 받아올 것으로 예상되는 레코드 수    
* **Cardinality** : 그 레코드의 수  
* 이 둘을 활용하여 **Cost**를 계산한다.  

### 2.3. Plan generator  
* cost기반으로 최적의 **실행 계획**을 생성한다.  

## 3. Row-source Generator  
* 옵티마이져가 생성한 **실행계획**을 SQL 엔진이 실행할 수 있는 코드로 생성.  


