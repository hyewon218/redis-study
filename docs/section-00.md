# Redis란?

**Re**mote **Di**ctionary **S**erver<br>
Open Source In-Memory Data Store written in ANSI-C

Key, Value 구조의 비정형 데이터를 저장하고 관리하기 위한 오픈 소스 기반의 비관계형 데이터 베이스 관리 시스템(DBMS)이다.
데이터베이스, 캐시, 메세지 브로커로 사용되며 인메모리 데이터 구조를 가진 저장소이다.

## Redis 특징
In-Memory 모든 데이터를 RAM에 저장 (백업 / 스냅샷 제외)
Single Threaded 단일 thread에서 모든 task 처리
Cluster Mode 다중 노드에 데이터를 분산 저장하여 안정성 & 고가용성 제공
Persistence RDB(Redis Database) + AOF(Append only file) 통해 영속성 옵션 제공
Pub/Sub Pub/Sub 패턴을 지원하여 손쉬운 어플리케이션 개발(e.g 채팅, 알림)

## Redis 장점
높은 성능 ⭐⭐
모든 데이터를 메모리에 저장하기 때문에 매우 빠른 읽기/쓰기 속도 보장 
Data Type 지원 ⭐
Redis에서 지원하는 Data type을 잘 활용하여 다양한 기능 구현 
클라이언트 라이브러리
Python, Java, JavaScript 등 다양한 언어로 작성된 클라이언트 라이브러리 지원 
다양한 사례 / 강한 커뮤니티
Redis를 활용하여 비슷한 문제를 해결한 사례가 많고, 커뮤니티 도움 받기 쉬움
  