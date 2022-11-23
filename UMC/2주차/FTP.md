
## 알 FTP 등을 통해 FTP 도 외부에서 접속가능하게 만들기


## `알ftp 다운로드`

![ftp](https://user-images.githubusercontent.com/48826098/203545584-71371ffa-cbac-4260-9b9d-2ad6aa10fcb6.jpg)

## `iptime 관리자 페이지 접속`

**[http://192.168.0.1/](http://192.168.0.1/) 로 접속해 iptime 관리자 페이지로 접속한다. → 관리도구 클릭**

![2](https://user-images.githubusercontent.com/48826098/203545899-6e00c066-be04-401e-aa43-964fb7d09d93.jpg)

**NAT/라우터 관리 → 포트포워드 설정**

![3](https://user-images.githubusercontent.com/48826098/203545908-30f97d8e-79c3-419f-a220-86e896b2b031.jpg)

![1](https://user-images.githubusercontent.com/48826098/203546212-07400e70-2a5b-42fb-b006-f80069ebed2e.jpg)

> fpt 새규칙을 만들어주었다. 외부 포트랑 내부 포트 둘 다 21로 해도 되지만 난 기숙사에 살고 있어서 혹시 몰라 외부 포트를 2121로 해주었다!
> 

 

## `알ftp 실행`

![2](https://user-images.githubusercontent.com/48826098/203544579-5d43ad6b-78c0-43e8-b99f-0f00d7f8924d.jpg)

> 서버 → 서버 실행 클릭
서버로 사용할 IP주소는 내부IP 주소를 입력한다
> 

![3](https://user-images.githubusercontent.com/48826098/203544589-65733391-ee82-491c-8e33-d67e1149e0ec.jpg)

> 서버를 만들고 실행시키면 접속하는 사람이 아직 없어서 0명으로 뜬다.
> 

![4](https://user-images.githubusercontent.com/48826098/203544598-72fe3d27-4d4c-44ac-8cb9-a3f6517819c1.jpg)

> 접속하기 클릭!!
FTP주소에는 외부IP주소를 입력하고, 포트포워딩 설정에서 지정했던 외부 포트 번호를 포트번호에 입력한다.
> 

![5](https://user-images.githubusercontent.com/48826098/203544612-76b0504a-1282-4db6-8e3d-e6c99879e498.jpg)

> 외부 접속 성공!
> 

