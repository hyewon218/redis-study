# Redis란?

**Key, Value** 구조의 비정형 데이터를 저장하고 관리하기 위한 오픈 소스 기반의 비관계형 데이터 베이스 관리 시스템(DBMS)이다.<br>
데이터베이스, 캐시, 메세지 브로커로 사용되며 인메모리 데이터 구조를 가진 저장소이다.

Redis는 캐시 기반의 인메모리 데이터 저장소로 분류하며 NoSQL 데이터베이스의 한 종류다.
Redis는 메모리에 데이터를 저장하고 조회하는 빠른 성능을 제공하고 데이터는 키-값(key-value) 형태로 저장한다.
데이터의 구조는 문자열, 해시, 리스트, Set, Sorted Set 등 다양하게 활용할 수 있다.
그 외로 메시지 브로커 기능도 제공된다.

## **Re**mote **Di**ctionary **S**erver<br>
**다수의 서버**가 사용하는 분산 환경의 서버가 **공통**으로 사용할 수 있는 **해시 테이블**<br>
- **Remote**라는 의미는 Redis가 각각의 서버 안에 로컬하게 존재하지 않고 다수의 서버에서 공통적으로 사용할 수 있도록 원격에 존재한다는 의미이다.<br>
- **Dictionary**라는 의미는 해시맵과 같이 key value 형태로 상수의 시간 복잡도로 사용이 가능하다.

## Open Source In-Memory Data Store written in ANSI-C
- **In-Memory** Data Store : 백업을 제외한 모든 데이터를 **RAM**에 저장
  - 램은 디스크에 비해 매우 **빠르기** 때문에 Redis는 기본적인 관계형 데이터베이스와 다른 구조와 특징을 갖는다.

<br>

### Redis 특징
- **In-Memory** : 모든 데이터를 **RAM**에 저장 (백업/스냅샷 제외)
- **Single Threaded** : 단일 thread에서 모든 task 처리
- **Cluster Mode** : 다중 노드에 데이터를 분산 저장하여 **안정성** & **고가용성** 제공
- **Persistence** : **RDB(Redis Database** + AOF(Append only file) 통해 영속성 옵션 제공
- **Pub/Sub** : Pub/Sub 패턴을 지원하여 손쉬운 어플리케이션 개발(e.g 채팅, 알림)

### Redis 장점
- 높은 성능 ⭐⭐<br>
모든 데이터를 메모리에 저장하기 때문에 매우 빠른 읽기/쓰기 속도 보장
- Data Type 지원 ⭐<br>
Redis에서 지원하는 Data type을 잘 활용하여 다양한 기능 구현
- 클라이언트 라이브러리<br>
Python, Java, JavaScript 등 다양한 언어로 작성된 클라이언트 라이브러리 지원 -> 백엔드와 쉽게 연동할 수 있다.
- 다양한 사례 / 강한 커뮤니티<br>
Redis를 활용하여 비슷한 문제를 해결한 사례가 많고, 커뮤니티 도움 받기 쉬움

### Redis 사용 사례
- Caching<br>
  - 임시 비밀번호(One-Time Password) 
  - 로그인 세션(Session)
- Rate Limiter<br>
  - Fixed-Window / Sliding-Window Rate Limiter(비율 계산기) 
- Message Broker<br> 
  - 메시지 큐(Message Queue)
- 실시간 분석 / 계산<br>
  - 순위표(Rank / Leaderboard)
  - 반경 탐색(Geofencing)
  - 방문자 수 계산(Visitors Count)
- 실시간 채팅 
  - Pub/Sub 패턴 

<br>

### Persistence
#### Persistence(영속성)
- Redis는 주로 캐시로 사용되지만 **데이터 영속성**을 위한 옵션 제공 
- **SSD**와 같은 영구적인 저장 장치에 데이터 저장

#### RDB(Redis Database)
- Point-in-time Snapshot -> 재난 복구(Disaster Recovery) 또는 **복제**에 주로 사용 
- 일부 데이터 유실의 위험이 있고, 스냅샷 생성 중 클라이언트 요청 지연 발생

#### AOF(Append Only File)
- Redis에 적용되는 Write 작업을 모두 **log로 저장**
- 데이터 유실의 위험이 적지만, 재난 복구시 Write 작업을 다시 적용하기 때문에 **RDB 보다 느림**

#### RDB + AOF
- 함께 사용하는 옵션 제공

<br>

### Caching
#### 캐싱(Caching)
- 데이터를 빠르게 읽고 처리하기 위해 **임시로 저장**하는 기술
- 계산된 값을 **임시로 저장**해두고, 동일한 계산 / 요청 발생시 다시 계산하지 않고 **저장된 값 바로 사용**
- 이 임시 데이터를 동일하거나 유사 요청이 왔을 경우 저장소에서 바로 읽어와서 응답을 하여 **성능 및 응답속도 향상**을 위한 기술
- **캐시(Cache) = 임시 저장소**

> API 서비스에서 요청(Request)이 왔을 경우, 연산을 수행하거나 DB의 데이터를 불러오거나 3rd Party 시스템에 인터페이스 하는 등<br>
> 특정 작업을 하여 데이터를 생성 후 다시 전달(Response)을 하게되는데 캐시를 이용해 특정 요청을 저장소에 임시로 저장해놨다가<br>
> 이후 동일한 응답을 해도 되는 요청이 왔을 경우 별도 연산 없이 바로 저장소에서 데이터를 가지고 응답을 하여 성능과 응답 시간을 개선할 수 있습니다.

#### 사용 사례
- CPU 캐시 : **CPU**와 **RAM**의 속도 차이로 발생하는 지연을 줄이기 위해 L1, L2, L3 캐시 사용
- 웹 브라우저 캐싱 : 웹 브라우저가 웹 페이지 데이터를 로컬 저장소에 저장하여 해당 페이지 재방문 시 사용
- DNS 캐싱 : 이전에 조회한 도메인 이름과 해당하는 IP 주소를 저장하여 재요청 시 사용
- 데이터베이스 캐싱 : 데이터베이스 조회나 계산 결과를 저장하여 재요청시 사용
- CDN : 원본 서버의 컨텐츠를 PoP 서버에 저장하여 사용자와 가까운 서버에서 요청 처리
- 어플리케이션 캐싱 : 어플리케이션에서 데이터나 계산 결과를 캐싱하여 반복적 작업

#### Cache Hit / Miss
<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/6721d7db-6358-462d-924c-ef404cdc2495" width="60%"/><br>

#### Cache-Aside pattern
<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/5b9576f2-306d-4673-a8f4-00edb1501a9c" width="60%"/><br>