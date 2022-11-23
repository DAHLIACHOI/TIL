
## 개인 컴퓨터 환경에서(Window or macOS) 포트포워딩을 통해 외부(4G, 5G 등)에서 접속하여 저번 주에 만들어둔 웹사이트 올려놓기.



> 현재 기숙사의 거주 중이며, 각각 방마다 다른 iptime 공유기를 사용하고 있음
미션 수행 후 포트포워딩 정보 삭제 했음
> 

---

## `iptime 관리자 페이지 접속`

[**http://192.168.0.1/](http://192.168.0.1/) 로 접속해 iptime 관리자 페이지로 접속한다. → 관리도구 클릭**

![2](https://user-images.githubusercontent.com/48826098/203545899-6e00c066-be04-401e-aa43-964fb7d09d93.jpg)

**NAT/라우터 관리 → 포트포워드 설정**

![3](https://user-images.githubusercontent.com/48826098/203545908-30f97d8e-79c3-419f-a220-86e896b2b031.jpg)

**새 규칙 생성**

![4](https://user-images.githubusercontent.com/48826098/203545916-38f559c5-b09e-4dd4-bdcf-07b1f527d40d.jpg)

> 난 spring을 사용했기 때문에 톰캣 서버인 8080포트를 사용해서 8080으로 지정해주었다.
> 

## `방화벽 해제 해주기`

**1)**

![10](https://user-images.githubusercontent.com/48826098/203545924-826f51a4-21ca-46ba-a087-a988e11c2382.jpg)

> 난 윈도우를 사용하고 있어서, window 보안 → 방화벽 및 네트워크 보호에 들어가면 도메인, 개인, 공용 네트워크가 모두 켜져 있는데 난 이 세 개를 모두 꺼주었다!!
> 

**2)**

![11](https://user-images.githubusercontent.com/48826098/203545932-125267cb-d8e3-460e-87d8-4c8f4003f24b.jpg)

> Window Defender 방화벽 → 고급설정 → 인바운드 규칙 → 새규칙 추가를 해서 8080포트를 연결을 허용해준다.
> 

![tomcat](https://user-images.githubusercontent.com/48826098/203545973-627008bf-1516-436c-b87f-ff290411a056.jpg)

> 이렇게 뜨면 잘 열어준 것!
> 

## `외부 IP확인`

![외부ip](https://user-images.githubusercontent.com/48826098/203545981-b29d42aa-5693-438d-be21-76f6c5f27fdc.jpg)

> 노란 부분이 외부 IP주소
> 

## `외부 연결`

> 외부IP:8080을 휴대폰 URL에 친다. 
폰 보면 와이파이로 연결되어있는데 포트포워딩을 진행한 와이파이가 아닌 옆 방 와이파이로 연결해서 진행했다.
> 

![KakaoTalk_20220929_203324053](https://user-images.githubusercontent.com/48826098/203545950-78c45912-d472-410f-9048-171b5439eec1.jpg)

> 잘 연결된 것을 볼 수 있다🙃
>