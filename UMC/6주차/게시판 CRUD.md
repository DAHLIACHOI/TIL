
## 1. 게시판 CRUD를 할 수 있는 API 개발</br>2. API 명세서 작성



### 프로젝트 생성

![1  파일 생성](https://user-images.githubusercontent.com/48826098/204083716-c5f8878e-c279-4209-b7d7-2f0694faa224.jpg)

필요한 dependency들을 미리 선언해주었다.

- java 11로 바꿈

### Spring boot Aws RDS MySQL 연동

JDBC API를 의존성에 추가해줘서 아래 코드를 추가해줘야 실행이 가능하다.

```
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://엔드포인트:3306/db이름
spring.datasource.username=root
spring.datasource.password=0000
```

### POST MAN으로 테스트 해보기

```java
@RestController
public class testController {

    @GetMapping("/test")
    public String test() {
        return "hello world";
    }
}
```

![postman test](https://user-images.githubusercontent.com/48826098/204083730-d7118e88-1224-4726-9d6e-de9d9185ba68.jpg)

### 게시판 API 명세서

![게시판 api 명세서](https://user-images.githubusercontent.com/48826098/204083735-e0e81c0c-0f63-49a3-891f-199042860dbe.jpg)

- 게시판 생성 (POST)
    
![post board](https://user-images.githubusercontent.com/48826098/204083728-1a609134-a182-4ea2-91bd-c4a33694e4a7.jpg)
    
- 게시판 조회 (GET)
    
![get board](https://user-images.githubusercontent.com/48826098/204083724-6d88c2e7-4366-472c-844d-b6a884a7a32e.jpg)
    
- 게시판 수정 (PUT)
    
![put](https://user-images.githubusercontent.com/48826098/204083733-d0e6036d-67e7-4efb-bc73-72e8f24cce90.jpg)
    
- 게시판 삭제 (DELETE)
    
![delete](https://user-images.githubusercontent.com/48826098/204083719-9c4a06d6-17e0-40e9-810e-1881e89e938d.jpg)
