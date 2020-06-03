

# Sharding.  
#### [샤딩?](http://blog.naver.com/PostView.nhn?blogId=kbm0996&logNo=221135040275&categoryNo=0&parentCategoryNo=0&viewDate=&currentPage=1&postListTopCurrentPage=1&from=postView)  
#### [영어 version](https://medium.com/@jeeyoungk/how-sharding-works-b4dec46b3f6)  

* **Vertical Partitioning** : 테이블에서 **특정 필드들에 대한 연산이 몰리는 경우** 그 부분을 따로 분리하여, **거기에 레플리케이션을 적용**.  

## 샤딩의 이점?  
#### [샤딩의 이점](https://www.digitalocean.com/community/tutorials/understanding-database-sharding)  
* 1. **모로리틱**한 Database와 달리, **Shared된 DB**에서 나눠진 양의 record만 full scan하면 되기에, 더 빠르다.  
 Another reason why some might choose a sharded database architecture is to speed up query response times. When you submit a query on a database that hasn’t been sharded, it may have to search every row in the table you’re querying before it can find the result set you’re looking for. For an application with a large, monolithic database, queries can become prohibitively slow. By sharding one table into multiple, though, queries have to go over fewer rows and their result sets are returned much more quickly.  
 



* 하나의 테이블을 레코드의 묶음으로, **수평 분할하여 여러 노드에 분산 저장**하는 기법.  
![image](https://user-images.githubusercontent.com/62331555/81693043-47480c80-949a-11ea-9eb9-4644b8d3ed6c.png)  

## 1. 샤딩  
* 반드시 샤딩을 먼저 도입할 필요가 없다. - **운영의 복잡도**를 증가시킨다.  
* 샤딩을 도입하기 전, read operation이 많이 요구된다면 **캐시**나 **레프리케이션(query-off)**을 먼저 고려한다.  

### 1. hash 기반 샤딩  
* shard key로 지정된 필드 값에 대하여 해쉬함수를 적용하여 나온 **hash value**를 **shard 갯수**에 대한 모듈러 연산을 적용하여,  
**샤드**를 선택한다.  

![image](https://user-images.githubusercontent.com/62331555/81694924-e53cd680-949c-11ea-8262-e5a8bdc4b42e.png)  

## resharding 문제  
* 샤드 중 하나가 다운되거나, 새로운 샤드가 추가되면 **shard function**이 갱신되기에 기존에 있던 데이터를 **마이그레이션**해야 한다.  

## 2. crc와 hashslot을 적용한 sharding 방식  
#### [Sharding 방법](https://engineering.linecorp.com/ko/blog/line-manga-database/)  
* **shard key 선택** : **cardinality**가 가장 낮을 것으로 예상되는 **primary key**를 선택한다.  

* hash function으로서, crc32와 같은 에러 검출 방법을 활용한다.  
* shard key로 member id를 선택한다.  
이 member id에 대한 crc32 결과 값을 hash slot의 갯수로 module 연산한다.  

* hash slot은 말 그대로 slot이다. 해쉬 결과 값이 hashslot number가 되며 이를 관리하는 shard를 찾아간다.  
### [redis에서도 key에 대한 crc적용 후 hashslot으로 shard를 찾는다.](http://redisgate.kr/redis/cluster/cluster_introduction.php)  

#### CRC : 원래 알던 것은, Data-link layer에서 **에러 검출**을 위하여 사용되는 방법으로, 나눗셈을 활용한다는 것까지 OK  
CRC로 생성된, 나머지를 payload에 부착하여 전송.  

* CRC32는 key를 32bit로 산출.  
* hash function time이 빠르다.  
* collision 확률이 낮으니까 쓰겟지?  
![image](https://user-images.githubusercontent.com/62331555/81700501-ac543000-94a3-11ea-96e4-86f8e9b583a9.png)  


```
$DB_SHARD_HASHSLOT = 65536    
-----------------------------------------------  
crc32(member_id) % $DB_SHARD_HASHSLOT             // 이 결과 2^16 이하의 수가 나온다. 이는 곧 슬롯이 된다.
-----------------------------------------------  
shard1 : 00000 – 08191                            // 해당 slot number를 가지고 있는 샤드에서 데이터를 관리한다.
shard2 : 08192 – 16383  
shard3 : 16384 – 24575  
shard4 : 24576 – 32767  
shard5 : 32768 – 40959  
shard6 : 40960 – 49151  
shard7 : 49152 – 57343  
shard8 : 57344 – 65535  
```


## Consistent Hashing  


