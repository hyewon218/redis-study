# AWS Elasticache for memcached
## vpc 설정
### vpc 생성
<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/e550b1c1-0274-4581-97ed-0ea39b5868ff" width="60%"/><br>
- ec2와 elasticache를 함께 쓸 것

<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/8942ad8f-e432-4525-8ad8-3e0020d40dd6" width="50%"/><br>
<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/1b981b4d-df5c-4e50-8cda-3f5f89d151fc" width="60%"/><br>

<br>

## memcached 설정
<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/b7962dd5-507f-4f25-9df7-ba83d85da917" width="60%"/><br>
<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/f13cb1a0-e96d-4bb2-b2ab-58f601ebc9c9" width="60%"/><br>
<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/95b0966b-5d66-4de3-ad46-b7f041ef8787" width="60%"/><br>
- memcached는 Node로 갯수를 늘릴 수 있다.<br>

<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/bfce0a97-9f91-42d0-be20-59cea182850f" width="60%"/><br>
<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/dc52b322-308c-47c9-8e5f-31324e3c1e0e" width="60%"/><br>

<br>

## ec2 설치
<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/1381e397-da27-4def-850e-09b8f6223d82" width="60%"/><br>
<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/f9ace443-b034-4d22-b5a2-c7488c0fb5bb" width="60%"/><br>
<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/3660a584-0991-458f-8bbe-ed27765d1542" width="60%"/><br>
- 서브넷 `public` 선택 

<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/82ef8301-9fc2-4792-942f-bc6dfe204dc7" width="60%"/><br>

<br>

## ec2 + memcached 연결
<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/96bc6b7b-1573-4c62-8ce4-6c3026f98f6c" width="60%"/><br>
<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/8c9b4645-723e-47f4-8f0a-4b0b9cb59492" width="60%"/><br>
<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/1364b553-483f-429e-a6af-42f40267b502" width="60%"/><br>
- 생성 에러<br>
  <img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/6fc5f081-be7d-4f68-9a9b-bdd498d41844" width="60%"/><br>
  <img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/5e8cf0a6-811a-4778-8396-0b184e9f0887" width="60%"/><br>
  <img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/6888bfb6-2e02-40e0-bdde-1d47e4808f09" width="60%"/><br>

<br>

### 재시도
<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/e6a768d0-22dd-4830-9b69-3e8ee02bed1e" width="60%"/><br>
- 연결 완료!<br>

<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/d2ede999-943d-49eb-b717-d09152a33a6c" width="60%"/><br>
- 다음 명령을 실행하여 인스턴스의 모든 패키지를 업데이트
- ```
  sudo apt-get update
  ```


<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/f83d61bb-2624-45f8-8b03-e587f7747079" width="60%"/><br>
- ```
  sudo apt-get install telnet
  ```
<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/28309f9f-2cfc-4257-a1f9-d2f8bcd170ba" width="60%"/><br>
- 구성 엔드포인트 복사
- memcached.ysd6fd.cfg.apn2.cache.amazonaws.com:11211

<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/3918da54-f9db-4f95-9fac-da9222acc8c5" width="60%"/><br>
- memcached 연결
- ```
  telnet memcached.ysd6fd.cfg.apn2.cache.amazonaws.com 11211
  ```
- `:` 지우기 주의!

<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/84da40c7-1172-49f1-a4c9-ecce676449c4" width="60%"/><br>
- private elasticache에 연결이 되었다.

## ec2와 elasticache 연결 성공!!!

<br>

### 설정
<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/29125fb1-eab6-463e-962b-a332c98834b8" width="60%"/><br>
-  ```shell
   set a 0 10 5
   ```
- 0 : 이 다음 글자부터
- 10 : 10초 동안 저장
- 5 : 다섯글자