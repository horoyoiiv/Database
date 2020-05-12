
# Integrity  

* 무결성  

#### DBMS에서의 무결성이란?  
* 데이터베이스 관리자에 의해 설계된 데이터 저장의 법칙.  

## 종류  

### 1. Domain Integrity  
* 레코드 필드의 값들이 "NOT NULL이어야 한다", 혹은 "ENUM 값 중 하나여야 한다"와 같은 도메인에 대한 제약 조건  

### 2. Entity Integrity  
* **기본키 제약조건**  
* 개체 무결성 : 기본키와 관련된다.   
* 테이블의 속성 중 **기본키로 지정된 필드**는 **NULL을 가질 수 없고**, **중복된 값을 가지면 안된다**.   
왜냐면 **기본키**는 **테이블에서의 레코드를 고유하게 식별하기 위하여 사용**되기 때문이다.  


### 3. Referential Integrity  

#### 2.1. Foreign Key  
* 외래키 : **분리된 두 테이블**이 관계를 맺는데 사용된다.  
다른 테이블(릴레이션)의 **기본키**를 자신의 필드로 가짐으로써, 이후 JOIN을 수행 시 

#### 2.2 참조 무결성  
* 한 테이블의 **foreign key**는 **유효한** 다른 테이블의 기본키를 가르키고 있어야 한다.  

이를 보장하기 위하여 **부모 테이블(기본키를 가진)**이 변경되거나, 삭제 시 자식테이블(FK를 가진)이 행동을 **Constraint**로 지정할 수 있다.  

```sql
CREATE TABLE pictures(
  pic_id int NOT NULL,
  user_id int NOT NULL, 
  PRIMARY KEY (pic_id),
  CONSTRAINT fk_pictures_to_user FOREIGN_KEY (user_id) REFERENCES user(user_id)
  ON DELETE [CASCADE] [RESTRICT / NO ACTION] [SET DEFAULT] 
  ON UPDATE [CASCADE] [RESTRICT / NO ACTION] [SET DEFAULT]
);
```

* **CASCADE** : 참조하던 레코드가 삭제 - 변경 시 동일하게 삭제 - 변경
* **NO ACTION** : 부모 테이블에서의 삭제, 변경을 제한한다. (RESTRICT와 동일)  
* **SET DEFAULT** : 부모 테이블의 레코드가 삭제 - 변경 시 DEFAULT로 지정한 값을 설정.  



















