# AWS elastic cache

## AWS Redis를 쓰는 이유?
- 90% Caching 때문

## 왜 `elasticache`일까?
- 배경 : **DB안정성**
- **GET REST API** 에 대한 비중을 줄이기 위해
- 특정 API에 집중되는 현상, 특히 데이터베이스로 select 문이 굉장히 많이 날아가는 현상들의 비중을 줄이기 위해 사용
- AWS elastic cache ? EC2에 Redis를 붙여서 쓸지?
- AWS 환경에서 Redis를 EC2에 설치하는 게 아니라 **elastic cache에 EC2를 붙여 AWS 환경 내에서** <br>
AWS가 설계한 Redis의 환경, 아니면 Memcache를 활용해서 EC2와 RDS를 안정성을 높일 수 있도록 한다.
- EC2의 RDS를 쓰지 않고, AWS가 설계한 Redis를 쓰고싶다면 추천
- 이미 EC2, AWS 클라우드 환경에 종속되어버린 환경

## aws elasticache 를 써야하는 이유
- 10만 request가 갑자기 100만 request가 왔을 때 내 서버는 잘 견딜 수 있나?<br>
  <img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/f1c2a772-2862-449e-8415-e2781df0bfcf" width="50%"/><br>
  - RDS는 터질 수 있음<br>

  <img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/e2257c89-f099-4045-a782-aac4bf8ef5bb" width="50%"/><br>
  - redis에 없으면 ec2 거쳐 rds에서 데이터 가져와서 redis에 저장 후 보내줌
  - redis가 터지면? ec2, rds 다 터질 수 있다.
  - redis를 도입함으로써 비용을 낮출 수는 있지만 꼭 안정성이 높아지는 것은 아니다. -> 서비스 안정성 면에서 잘 설계된 elasticache 도입

## Memcached vs Redis
둘 다 메모리 데이터베이스<br>
- Memcached가 먼저 나오고 Memcached의 영향을 받아 redis가 2009년에 나옴
- redis가 Memcached의 상위 버전(다양한 기능이 많음)<br>
  <img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/81c2c934-b242-4dd4-b3aa-12314cd4551f" width="50%"/><br>

- **Memcached** : 캐싱만을 위한 서비스
- **Redis** : NoSQL 데이터베이스 
  - Snapshots(일정부분 SSD 하드에 데이터 넣음), Replication 과 같은 안정성에 대한 옵션들이 있다.
  - pub/sub - 대용량 처리를 위한 간단한 구조도 만들 수 있다.

## 사용 목적
<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/629b8a54-abd5-4388-b9dc-990e2bd40926" width="50%"/><br>
<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/b22b3b15-197b-4321-8ee9-f043049ab0f0" width="50%"/><br>

## AWS 네트워크 - vpc 설정
<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/5f936262-5dde-4b58-8aea-57994d72df42" width="50%"/><br>
- public으로 접속이 불가하기 때문에 ec2와 연결을 해야한다.