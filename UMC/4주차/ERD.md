## ERD

- ‘Entity Relationship Diagram’
- ‘존재하고 있는 것(Entity)들의 관계(Relationship)을 나타낸 도표(Diagram)
== 데이터 들의 관계를 나타낸 도표

![erd표기방식](https://user-images.githubusercontent.com/48826098/203613646-473ec53c-d401-4cdc-ae4c-ada0b6e0846e.jpg)

- A 테이블의 기본키를 B테이블이 가지고 있다면 A테이블은 부모 테이블, B테이블은 자식 테이블을 뜻함

### 관계선 종류

- 실선 : 식별관계
-  부모 테이블의 PK가 자식테이블의 FK/PK가 되는 경우
-  부모가 있어야 자식이 생기는 경우
-  외래키를 기본키로 사용하는 관계
- 점섬 : 비식별관계
-  부모 테이블의 PK가 자식 테이블의 일반 속성이 되는 경우
-  부모가 없어도 자식이 생기는 경우

### 숫자

1) 정수

- tinyint()
- smallint()
- mediumint()
- int()
- biginit()

2) 실수

- decimal()
- double()
- float()

### 문자

- varchar()
- char()

### 날짜, 시간

- date() → 1000-01-01 ~ 9999-12-31
- datetime() → 1000-01-01 00:00:00.000000 ~ 9999-12-31 23:59:59.999999
- timestamp() = datetime() + timezone

### 배달의 민족

> ERDCLOUD 사용했는데 NULL 허용 여부를 확인 할 수 없어서,,임의로 위치를 바꿔서 작성했다
> 

![배민erd](https://user-images.githubusercontent.com/48826098/203613663-6d502bb8-fbdb-451c-92ab-03c6ab76d9df.jpg)
