

# Query-off  

### [1. 조대협님 블로그](https://bcho.tistory.com/tag/Change%20Data%20Capture)  


## 1. 퍼포먼스 향상을 위한 복제 서버 구축  

1. 하나의 **Master Node**와 여러 개의 **Slave Node**를 구성한다.  
* **Master Node** : DB에 대한 Insert, Update, Delete 연산을 담당한다.  
* **Slave Node** : DB에 대한 Select 연산을 담당한다.  

2. 그렇기에 **어플리케이션**에서 읽기와 쓰기 로직을 분리하여 구현하여야 한다.(읽고 쓰는 곳이 다르기에)  

![image](https://user-images.githubusercontent.com/62331555/81503267-9a488500-931d-11ea-82d9-f84ffb131517.png)  

## 2. Connection Pool  
* **Connection Pool**이란 **Slave 클러스터**와 **어플리케이션** 사이에 위치하며 **LB**와 **HA**를 지원한다.  


## 3. Master와 Slave 사이의 "동기화" 방법  

* DB의 연산과정에서 발생하는 **BackLog**를 사용한다.  
* Back log , ops log : 데이터베이스는 Disk에 데이터를 쓰기 전, (이론 상으로 안전해야 하는) Log 파일에 먼저 연산 내용을 저장하여  
**UNDO, REDO 라는 Recovery에 사용**한다. 이를 **WAL**이라고 한다.  

### [MongoDB의 oplog](https://www.compose.com/articles/the-mongodb-oplog-and-node-js/)  

* Master에서 발생한 연산에 대한 backlog를 직접 Slave에 전송해주는 **Push방식**의 query off 동기화  
* Slave가 직접 요청하여, backlog 정보를 받아와서 **replay**하는 방식의 **Pool방식**의 query off 동기화  



















