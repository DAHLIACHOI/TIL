<aside>
💡 **Standard Mission**

1. AWS Elastic IP 적용하여 http 외부접속 가능하게 Nginx, php, mysql 설치
2. RDS로 데이터베이스 (MySQL) 생성 후 외부(DataGrip, Workbench 등)에서 접속가능하게 만들기
3. domain 연결 (가비아, 후이즈 등)
4. https 적용(Let's Encrypt)

</aside>


### `ec2 인스턴스 생성`

![1](https://user-images.githubusercontent.com/48826098/202844173-cd2b4101-4d81-45c7-9e79-dde858bc8963.jpg)

![2](https://user-images.githubusercontent.com/48826098/202844177-7e2697bd-9fbe-428a-97b1-6101a581f921.jpg)

### `WinSCP 다운로드`

![3](https://user-images.githubusercontent.com/48826098/202844178-2f34ade0-79ec-42bd-9b12-6d75e76f0960.jpg)

![4](https://user-images.githubusercontent.com/48826098/202844181-38d9ee35-6bc5-4712-9d69-7fd72c124fd4.jpg)

> AWS에서 생성한 서버를 연결했다.
난 ubuntu로 설정했기 때문에 사용자 이름을 ubuntu로 했다
고급 설정에서 key 폴더를 지정해주어야 한다!
> 

![5](https://user-images.githubusercontent.com/48826098/202844184-4e22ce5e-6162-4f4b-868d-dd7d04d67cfe.jpg)

![6](https://user-images.githubusercontent.com/48826098/202844190-9042f380-bb49-4a02-94d8-2af70add199c.jpg)

> http로 열기 위해서 http 포트를 인바운드 규칙에 추가해주었다.
> 

![7](https://user-images.githubusercontent.com/48826098/202844193-1c4f36cb-6eec-4587-85fb-6b6d451fd4df.jpg)

> nginx를 설치해서 nginx가 정상적으로 뜬 것을 확인 할 수 있다.
> 

![9](https://user-images.githubusercontent.com/48826098/202844209-86164317-d815-425a-8eb3-87af8ebe8233.jpg)

> index.php 파일을 만들어서 웹에 창을 띄운 모습
> 

![10](https://user-images.githubusercontent.com/48826098/202844211-878c96a7-a267-4a5b-ac15-4f6824c76139.jpg)

> MySQL 외부접속을 하기!
root계정으로 하면 보안상에 문제가 있을 수도 있다고 해서 yejiserver라는 유저를 따로 생성해줬다.
> 

![11](https://user-images.githubusercontent.com/48826098/202844204-41b188e5-ad4c-42fc-93ac-a3c312e44929.jpg)

> 권한 설정 해주기
> 

![11 mysql workbench](https://user-images.githubusercontent.com/48826098/202844215-c053b133-0ae7-4dcb-a5c6-d4f04047f569.jpg)

> 난 Workbench가 이미 깔려 있어서 그냥 workbench로 실행해줬다.
정상적으로 잘 연결된 것을 볼 수 있다.
물론 이거 하기 전에 aws 인바운드 규칙에 mysql포트도 열어주었다.
> 

### `도메인 연결하기`

![12](https://user-images.githubusercontent.com/48826098/202844225-2f6de58b-b920-4345-a5d8-21fd047d1600.jpg)

> 가비아에서 dahlidchoi.shop이라는 도메인을 사서 ip주소가 아닌 도메인으로 연결한 모습니다!
가비아 안에서 DNS설정에 들어가서 IP주소랑 연결해주었다.
> 

### `HTTPS 적용`

![13](https://user-images.githubusercontent.com/48826098/202844232-26828967-0093-4c2c-b1e3-6f7f385a8ef2.jpg)

---

**참고한 사이트**

[MySQL 외부접속 - MySQL Workbench 사용](https://jminie.tistory.com/101)

[AWS EC2 Ubuntu 서버에 도메인 연결하기(가비아)](https://velog.io/@banjjoknim/AWS-EC2-Ubuntu-%EC%84%9C%EB%B2%84%EC%97%90-%EB%8F%84%EB%A9%94%EC%9D%B8-%EC%97%B0%EA%B2%B0%ED%95%98%EA%B8%B0)

[How to Secure Nginx with Lets Encrypt on Ubuntu 20.04 with Certbot?](https://www.youtube.com/watch?v=R5d-hN9UtpU)