

# Sharding  
[Digital ocean](https://www.digitalocean.com/community/tutorials/understanding-database-sharding)  

## Sharding의 장점  

1. Scale-out이 용이하다.  
2. Query response time이 줄어든다. : 상대적으로 적은 양의 rows만 조회하기에  

## Sharding의 단점  

1. 설계가 복잡하다. : 어떤 것을 shard key로 할지, 새 노드가 추가되면 어떻게 대처할지...  


#### 1. shard key  

* 데이터가 어떤 shard, chunk에 저장될지 결정하는 field  


#### 2. Vertical Partitioning  
Vertical partitioning divides a table into multiple tables that contain fewer columns.

The two types of vertical partitioning are **normalization** and **row splitting**:

Normalization is the standard database process of removing redundant columns from a table and putting them in secondary tables that are linked to the primary table by primary key and foreign key relationships.

Row splitting divides the original table vertically into tables with fewer columns. Each logical row in a split table matches the same logical row in the other tables as identified by a UNIQUE KEY column that is identical in all of the partitioned tables. For example, joining the row with ID 712 from each split table re-creates the original row. Like horizontal partitioning, vertical partitioning lets queries scan less data. This increases query performance. For example, a table that contains seven columns of which only the first four are generally referenced may benefit from splitting the last three columns into a separate table. Vertical partitioning should be considered carefully, because analyzing data from multiple partitions requires queries that join the tables.

Vertical partitioning also could affect performance if partitions are very large.  

* Vertical Partitioning은 rows의 특정 column에 대한 연산이 집중된다면 그 부분을 splitting한다.  


## 1. Hash Sharding  
[Hashed Sharding in MongoDB](https://docs.mongodb.com/manual/core/hashed-sharding/#hashvalue)  

[Cardinality](https://en.wikipedia.org/wiki/Cardinality_(SQL_statements))  

#### 1. hashing에 사용할 shard key의 조건  
1. Cardinality가 높아야 한다. - uniqueness가 높아야 한다.  
2. static해야 한다. - 자주 바뀌면 안된다.  

#### 2. 단점  
1. 새 노드가 추가되면 **rehashing**, **resharding**을 통한 **Migration**이 필요해진다.  
2. 이는 곧 **downtime으로 귀결**된다.  

#### 3. 장점  
1. 수학적인 distribution이기에 추가적인 mapping table이 없어도 된다.  
2. evenly distribution의 확보가 용이하다.  



## 2. Ranged Based Sharding  

* shard key의 range를 바탕으로 shard에 분산  
* 예) 알파벳 이름의 앞 글자로 26의 shard 생성  

![image](https://user-images.githubusercontent.com/62331555/80139953-3ebe8d80-85e2-11ea-98a9-c2b8cbbc1eb9.png)  
[ref](https://medium.engineering/how-medium-detects-hotspots-in-dynamodb-using-elasticsearch-logstash-and-kibana-aaa3d6632cfd)  

#### 2. 단점   
1. evenly distribution의 보장이 어려움 : hotspot 발생  

#### 3. 장점  
1. 설계가 쉽다.  



## 3. Directory Based Sharding  

 * shard key는 **lookup table**에 매핑되어 있는 shard 주소에 저장된다.  
 * range based sharding에서 A에 몰리고 B C가 적다면 아래와 같은 lookup table 가능.  
 
 ```
 shard key | shard id
 ---------------------
    A      |   1 
  --------------------
    B      |   2
  --------------------
    C      |   2
  --------------------   
 ```
 ![image](https://user-images.githubusercontent.com/62331555/80140558-17b48b80-85e3-11ea-85c8-5f24e1036070.png)  
 
#### 1. 단점  

#### 2. 장점  
1. range based diretory보다 유연하다.  
2. 

 



