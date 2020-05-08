

# Index  

# 1. B-tree  
  
* 인덱스는 RDBMS에서 SELECT query 성능을 향상시키기 위한, **추가적인 자료구조**이다.  
```sql
CREATE INDEX myindex    // 인덱스 이름
ON user(name);          // 테이블 명(필드 리스트...)
```

### 1. 인덱스를 만들기 위하여 사용되는 B-tree  
* Balanced tree  
* 자식 노드는 둘 이상이 될 수 있기네 Binary Tree는 아님.  
* 하지만 **정렬된 상태를 유지**한다.  
* 인덱스를 생성하고자 선택된 **필드**를 기준으로 B-tree를 형성  

### 2. 동작  
* Degree(정도)에 따라 **하나의 노드**가 가질 수 있는 **키 컬럼**이 결정됨.  
![image](https://user-images.githubusercontent.com/62331555/81421164-fb405380-918b-11ea-8e27-0b8395201af4.png)  

* **non-leaf 노드**는 자식 노드에 대한 주소 정보를 가진다.  
* **leaf 노드**는 해당 키 컬럼과 매핑되는 **실제 레코드 주소**를 가르킨다.  


### 3. 삽입  
[B-tree 동작방식](https://potatoggg.tistory.com/174)  

* 하나의 노드에 포함된 키 컬럼 수가 Degree 이상되는 경우 **스플릿**을 수행.  
* **중간값**을 기준으로 스플릿을 수행한 후 그 **중간값**을 부모로 올려보내서, 재귀적으로 **스플릿**을 수행.  

### 4. 왜 다른 트리도 아니고, B-tree인가?  

* B-tree는 하나의 노드가 가질 수 있는 **키**는 Degree에 의해 결정되며, **하나의 노드에 많은 키를 저장가능**.  
* 하나의 노드를 **하나의 Page 단위**로 저장하여, 디스크 I/O를 최소화할 수 있기 때문이다.  

![image](https://user-images.githubusercontent.com/62331555/81421917-35f6bb80-918d-11ea-85e1-8c7ba011e9fd.png)   


# 2. 인덱스  
[인덱스](https://idea-sketch.tistory.com/43?category=547413)  

* 만일 인덱스가 없다면, WHERE절 뒤, 혹은 ON절(JOIN) 뒤의 조건을 만족하는 **레코드**를 찾기위하여 **리니어 서치**를 해야 한다.  
* B-tree로 구성된 인덱스를 탐색함으로써, **트리의 Heigth에 비례하는 서치 타임을 확보**할 수 있다.  


#### [장점]  
1. 빠른 SELECT 타임을 확보할 수 있다.  

#### [단점]  
1. 그외, UPDATE, INSERT, DELETE 구문의 경우 **원래의 데이터 파일 뿐만 아니라, 인덱스 파일에도 수정 연산을 해야**하기에 더 느리다.  
2. 인덱스 자체로도, 디스크 용량을 잡아 먹는선다.  
3. 데이터가 많은 경우, **인덱스 생성 시간**이 오래 걸릴 수 있다.  

#### [결론]  
1. 인덱스를 생성할 **필드**는 **SELECT 혹은 JOIN 조건절에 자주 사용**되면서, **변경은 자주 발생하지 않는** 필드에 적용해야 한다.  
2. 하지만 더 중요한 것은 인덱스 적용 후 **성능 측정을 실제로 해보고** 향상된 성능이 다른 Trade-off에 비해 가치가 있는지 판단 후 사용 결정.  



# 3. Clustered Index  

* Clustered Index의 경우 **이 인덱스가 정렬을 유지하는 순서대로, 실제 물리적 데이터 파일도 정렬된 상태를 유지**하는 것.  
* 그렇기에 하나의 테이블에는 **하나의 Clustered Index**만 가능하다.  
* 또한, 인덱스의 정렬 순서대로, 데이터 파일이 정렬되기에 -> **leaf node를 데이터 파일의 레코드 그 자체**가 된다.  

* InnoDB에서는 **PK를 기준으로 자동으로 Clustered Index를 생성**.  

* 그외, **Non Clustered Index**는 B-tree에서의 Leaf node의 키 값대로, 데이터 파일이 정렬되지 않기에 레코드 주소를 가져야 한다.  



* With a clustered index the rows are stored physically on the disk in the same order as the index. Therefore, there can be only one clustered index.

With a non clustered index there is a second list that has pointers to the physical rows. You can have many non clustered indices, although each new index will increase the time it takes to write new records.

It is generally faster to read from a clustered index if you want to get back all the columns. You do not have to go first to the index and then to the table.

Writing to a table with a clustered index can be slower, if there is a need to rearrange the data.



* 클러스터링 인덱스 구조를 보면 클러스터링 테이블의 구조 자체는 일반 B-Tree와 많이 비슷하게 닮아 있습니다. 하지만 B-Tree의 리프 노드와는 달리 클러스터링 인덱스의 리프 노드에는 레코드의 모든 컬럼이 같이 저장되어 있습니다. 즉 클러스터링 테이블은 그 자체가 하나의 거대한 인덱스 구조로 관리되는 것입니다.

출처: https://12bme.tistory.com/149 [길은 가면, 뒤에 있다.]
[클러스터링 인덱스](https://12bme.tistory.com/149)  
