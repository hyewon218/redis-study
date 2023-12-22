# Cache 전략 
속도를 빠르게 하기 위함

## lazy loading
<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/1fdce329-ccad-4786-b48b-df6d4c1836b2" width="60%"/><br>
#### Cache Miss
- 속도가 느려진다.

## write through
- Cache Miss 의 가능성을 줄이기 위해

<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/60649219-75a4-4011-95a7-c28803300cab" width="60%"/><br>

- 서버에서 데이터베이스 데이터를 가져와서 받은 데이터를 redis 에 넣는 과정

<br>

## REST API 캐싱해보기 - 시퀀스다이어그램

<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/bfa6e4d2-f163-4e72-9556-1cead8f25808" width="60%"/><br>

<img src="https://github.com/hyewon218/kim-jpa2/assets/126750615/b92816ae-d098-4ae1-96aa-d2cdcaf3ed90" width="60%"/><br>
- 목적 : database가 터지는 것을 방지하고 싶다! / get에 대한 비율을 줄이고 싶다!
- 데이터베이스로 가는 코드를 줄이려고 한다.
- 레디스 키 no : 레디스의 key가 없으면 데이터베이스에서 가져와 다시 레디스에 저장하고 보낸다. / 보낸 후 저장할 수도 있다.