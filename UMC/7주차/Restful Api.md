
## 지난번 개발했던 API를 Framework에 맞춰서 Restful API로 개발, API 명세서도 포함


➕ 듀얼 모니터로 확장해서 진행해서 그런지 캡쳐 화면이 너무 깨진다….😭

### user 템플릿 테스트 해보기

- PATCH할 때 오류 발생했음

![user patch 500 error](https://user-images.githubusercontent.com/48826098/204151108-311c0d61-9c93-46ba-b616-e80f83db1467.jpg)

**👉 해결 방법**

user 클래스 위에 `@NoArgsConstructor` 선언해준다.

```java
@Getter // 해당 클래스에 대한 접근자 생성
@Setter // 해당 클래스에 대한 설정자 생성
@AllArgsConstructor // 해당 클래스의 모든 멤버 변수(userIdx, nickname, email, password)를 받는 생성자를 생성
@NoArgsConstructor
public class User {
    private int userIdx;
    private String email;
    private String password;
    private String nickname;
}
```

`@NoArgsConstructor` : 파라미터가 없는 기본 생성자를 생성해줌

`@AllArgsConstructor` : 모든 필드 값을 파라미터로 받는 생성자를 만들어줌

---

- **`강의 들으면서 정리한거`**
    - GET/DELETE는 바디 필요 없음
    - 명사-명사 구분자는 하이픈(-) 사용
    - 대문자 금지
    - HTTP 메서드는 실제 DB동작을 기준으로 한다.
    → 회원 탈퇴 API : PATCH
    
    ▪️ROUTER → CONTROLLER → PROVIDER/SERVICE → DAO 이렇게 상위 관계를 유지한다.
    
    - **router** : restful하게 설계해야됨, `/users/:useridx` 이런식으로 경로 설정해주는 걸 여기서 해주는 거, 이 뒤에 controller로 연결해주는거임 controller로 리퀘스트 값을 전달
    - **controlle**r : 밑으로 전달해줌, route에 path variable, query string, body를 가져와서 넘겨주는거임 (파라미터를 통해서 전달하게 됨), validation 역할도 함
    - **service/provider** : DB connection이 일어남, transaction도 일어남
    - **dao** : 실질적인 query작성, 실행
    
    ➕ provider, service차이점
    - provider → select
    - service → insert, delete, update 할 때 사용
    

---

### API 명세서

![API명세서](https://user-images.githubusercontent.com/48826098/204151106-fef1679d-a0d5-4c3c-a1a9-ad793c45e3d6.jpg)

- 게시판 삭제를 원래 delete로 하려고 했는데 세미나에서 delete하는 것보다 status 값을 바꾸는게 더 좋다고 했고, 동작하는 형태로 API를 작성하라고 해서 DELETE대신에 PATCH사용했다

[API_SHEET_TEMPLATE.xlsx](https://docs.google.com/spreadsheets/d/17p8fMu5eg7nQWAjmocq2y_5nel8wtira/edit?usp=sharing&ouid=118394170528535521094&rtpof=true&sd=true)

```sql
CREATE TABLE board (
	`idx` 		INT UNSIGNED 		NOT NULL 	AUTO_INCREMENT 	COMMENT '인덱스',
    `title` 	VARCHAR(255) 		NOT NULL 	COMMENT '제목',
    `content` 	TEXT 		NOT NULL 	COMMENT '내용',
    `password` 	VARCHAR(200) 		NOT NULL 	COMMENT '비밀번호',
	`writer` 	VARCHAR(45) 		NOT NULL 	DEFAULT 'default name' COMMENT '작성자',
    `createdAt` TIMESTAMP 			NOT NULL 	DEFAULT CURRENT_TIMESTAMP COMMENT '생성일자',
    `updatedAt` TIMESTAMP 			NOT NULL 	DEFAULT current_timestamp on update current_timestamp COMMENT '갱신(업데이트)일자',
    `deleted` 	VARCHAR(1) 			NOT NULL 	DEFAULT 'N' COMMENT 'N : 삭제 안됨, Y : 삭제됨',
    PRIMARY KEY (idx)
)
```

### DB연결

```
server.port=9090
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/umcboard?serverTimezone=UTC&characterEncoding=UTF-8
spring.datasource.username=root
spring.datasource.password=****
```

> AWS RDS 결제돼서…ㅋㅋㅋㅋㅋㅋ 그냥 로컬로 DB에 연결했다….😅
> 

➕ 가장 상위에 `@RequestMapping("/boards")` 작성함

## 게시판 생성 (POST)

- controller
    
    ```java
    @ResponseBody
        @PostMapping("/write") // (/boards/write)
        public BaseResponse<PostBoardRes> createBoard(@RequestBody PostBoardReq postBoardReq) {
            try {
                PostBoardRes postBoardRes = boardService.createBoard(postBoardReq);
                return new BaseResponse<>(postBoardRes);
            } catch (BaseException exception) {
                return new BaseResponse<>((exception.getStatus()));
            }
        }
    ```
    
- service
    
    ```java
    // 새로운 게시판 등록 (POST)
        public PostBoardRes createBoard(PostBoardReq postBoardReq) throws BaseException {
            try {
                int idx = boardDao.createBoard(postBoardReq);
                return new PostBoardRes(idx);
            } catch (Exception exception) {
                throw new BaseException(DATABASE_ERROR); // alt+enter해서 앞에 BaseResponseStatus 생략해줌
            }
        }
    ```
    
- dao
    
    ```java
    // 게시판 생성
        public int createBoard(PostBoardReq postBoardReq) {
            String createBoardQuery = "insert into Board (title, content, password, writer) VALUES(?,?,?,?)";
            Object[] createBoardParams = new Object[]{postBoardReq.getTitle(), postBoardReq.getContent(), postBoardReq.getPassword(), postBoardReq.getWriter()};
            this.jdbcTemplate.update(createBoardQuery, createBoardParams);
    
            String lastInsertIdQuery = "select last_insert_id()";
            return this.jdbcTemplate.queryForObject(lastInsertIdQuery, int.class);
        }
    ```
    

![새 게시판 생성](https://user-images.githubusercontent.com/48826098/204151119-a8a258d6-7c4c-4760-bd0e-13d7b4fa7248.jpg)

- 생성 확인

![게시판 생성 db](https://user-images.githubusercontent.com/48826098/204151114-4004d268-9fb9-43df-9198-c464f13c0cb0.jpg)

## 게시판 조회(GET) [전체 게시판 조회, 해당 작성자 게시판 조회]

→ 비밀번호는 굳이 안보여도 될 듯하여 조회하지 않았다!

- controller
    
    ```java
    @ResponseBody
        @GetMapping("")
        public BaseResponse<List<GetBoardRes>> getBoards(@RequestParam(required = false) String writer) {
            try {
                if (writer == null) {
                    List<GetBoardRes> getBoardRes = boardProvider.getBoards();
                    return new BaseResponse<>(getBoardRes);
                }
                List<GetBoardRes> getBoardRes = boardProvider.getBoardsByWriter(writer);
                return new BaseResponse<>(getBoardRes);
            } catch (BaseException exception) {
                return new BaseResponse<>((exception.getStatus()));
            }
        }
    ```
    
- provider
    
    ```java
    // Boards 정보 조회
        public List<GetBoardRes> getBoards() throws BaseException {
            try {
                List<GetBoardRes> getBoardRes = boardDao.getBoards();
                return getBoardRes;
            } catch (Exception exception) {
                throw new BaseException(DATABASE_ERROR);
            }
        }
    
        // 해당 writer의 게시판 정보 조회
        public List<GetBoardRes> getBoardsByWriter(String writer) throws BaseException {
            try {
                List<GetBoardRes> getBoardRes = boardDao.getBoardsByWriter(writer);
                return getBoardRes;
            } catch (Exception exception) {
                throw new BaseException(DATABASE_ERROR);
            }
        }
    ```
    
- dao
    
    ```java
    // 모든 게시판 정보 조회
        public List<GetBoardRes> getBoards() {
            String getBoardsQuery = "select * from board where deleted = 'N'";
            return this.jdbcTemplate.query(getBoardsQuery,
                    (rs, rowNum) -> new GetBoardRes(
                            rs.getInt("idx"),
                            rs.getString("title"),
                            rs.getString("content"),
                            rs.getString("writer"))
            );
        }
    
        // 해당 writer를 갖는 게시판 정보 조회
        public List<GetBoardRes> getBoardsByWriter(String writer) {
            String getBoardsByWriterQuery = "select * from board where writer = ? AND deleted = 'N'";
            String getBoardsByWriterParams = writer;
            return this.jdbcTemplate.query(getBoardsByWriterQuery,
                    (rs, rowNum) -> new GetBoardRes(
                            rs.getInt("idx"),
                            rs.getString("title"),
                            rs.getString("content"),
                            rs.getString("writer")),
                    getBoardsByWriterParams);
        }
    ```
    

![전체 게시판 조회](https://user-images.githubusercontent.com/48826098/204151125-a53467e1-f6e0-434b-8659-235f111f7cd5.jpg)

전체 게시판 조회

![해당 writer 게시판 조회 (쿼리 스트링 사용)](https://user-images.githubusercontent.com/48826098/204151127-0a240671-fc46-4884-8d69-e9c853431f1f.jpg)

쿼리 스트링을 사용해서 해당 작성자의 게시판만 조회

## 특정 idx의 게시판 조회(GET)

→ 위에서 특정 writer의 게시판을 조회할 때는 query string을 사용했는데, 이번엔 path variable을 사용해서 조회한다.

- controller
    
    ```java
    @ResponseBody
        @GetMapping("/{idx}")
        public BaseResponse<GetBoardRes> getBoard(@PathVariable("idx") int idx) {
            try {
                GetBoardRes getBoardRes = boardProvider.getBoard(idx);
                return new BaseResponse<>(getBoardRes);
            } catch (BaseException exception) {
                return new BaseResponse<>((exception.getStatus()));
            }
        }
    ```
    
- provider
    
    ```java
    // 해당 idx를 갖는 게시판 정보 조회
        public GetBoardRes getBoard(int idx) throws BaseException {
            try {
                GetBoardRes getBoardRes = boardDao.getBoard(idx);
                return getBoardRes;
            } catch (Exception exception) {
                throw new BaseException(DATABASE_ERROR);
            }
        }
    ```
    
- dao
    
    ```java
    // 해당 idx를 갖는 게시판 조회
        public GetBoardRes getBoard(int idx) {
            String getBoardQuery = "select * from board where idx = ? AND deleted = 'N'";
            int getBoardParams = idx;
            return this.jdbcTemplate.queryForObject(getBoardQuery,
                    (rs, rowNum) -> new GetBoardRes(
                            rs.getInt("idx"),
                            rs.getString("title"),
                            rs.getString("content"),
                            rs.getString("writer")),
                    getBoardParams);
        }
    ```
    

![해당 idx사용해서 조회](https://user-images.githubusercontent.com/48826098/204151126-74eabb20-3584-4e60-acf5-c1d48e68f871.jpg)

> Path Variable로 값을 넘겨주었음, 사실 그냥 숫자 써도 된다..
query string이랑 구분하고 싶어서~
> 

## 게시판 수정 (PUT)

- controller
    
    ```java
    @ResponseBody
        @PutMapping("/update/{idx}")
        public BaseResponse<String> updateBoard(@PathVariable("idx") int idx, @RequestBody PutBoardReq putBoardReq){
            try {
                boardService.updateBoard(putBoardReq);
                String result = "게시판이 수정이 완료되었습니다.";
                return new BaseResponse<>(result);
            } catch (BaseException exception) {
                return new BaseResponse<>((exception.getStatus()));
    
            }
        }
    ```
    
- service
    
    ```java
    // 게시판 수정 (PUT)
        public void updateBoard(PutBoardReq putBoardReq) throws BaseException {
            try {
                if(boardDao.isCheckedPwUpdate(putBoardReq.getIdx(), putBoardReq.getWriter(), putBoardReq.getPassword()) != 1) {
                    throw new BaseException(INCORRECT_PASSWORD);
                }
                int result = boardDao.updateBoard(putBoardReq);
                if (result == 0) {
                    throw new BaseException(UPDATE_FAIL_BOARD);
                }
            } catch (NullPointerException exception) {
                throw new BaseException(DATABASE_ERROR);
            }
        }
    ```
    
- dao
    
    ```java
    public int updateBoard(PutBoardReq putBoardReq) {
            String updateBoardQuery = "update board set title = ?, content = ? where idx = ?";
            Object[] updateBoardParams = new Object[]{putBoardReq.getTitle(), putBoardReq.getContent(), putBoardReq.getIdx()};
    
            return this.jdbcTemplate.update(updateBoardQuery, updateBoardParams);
        }
    
    public int isCheckedPwUpdate(int idx, String writer, String password) {
            String getPasswordQuery = "select exists (select * from board where idx = ? AND writer = ? AND password = ?)"; //해당 조건에 맞는 게시판이 있는지 확인, 있으면 1, 없으면 0 반환
            Object[] updateBoardParams = new Object[]{idx, writer, password};
            return this.jdbcTemplate.queryForObject(getPasswordQuery, int.class, updateBoardParams);
        }
    ```
    

![게시판 수정 전](https://user-images.githubusercontent.com/48826098/204151115-df4caab3-8694-4fef-891e-f6978450f760.jpg)

![게시판 수정](https://user-images.githubusercontent.com/48826098/204151118-ffa6f694-536b-41f0-8ce9-82e50f32487d.jpg)

![게시판 수정 후](https://user-images.githubusercontent.com/48826098/204151117-a553391f-794a-4458-b494-18e9ee199ce3.jpg)

**➕ 비밀번호 일치하지 않을 때 (미리 정보 넣어둠!)**

![수정 비밀번호 일치 노](https://user-images.githubusercontent.com/48826098/204151121-06d14472-c8a0-42e8-8fd8-b817b53ed3ec.jpg)

## 게시판 삭제 (PATCH)

- controller
    
    ```java
    @ResponseBody
        @PatchMapping("/delete/{idx}")
        public BaseResponse<String> deleteBoard(@PathVariable("idx") int idx, @RequestBody PatchBoardReq patchBoardReq) {
            try {
                boardService.deleteBoard(patchBoardReq);
                String result = "게시판 삭제가 완료되었습니다.";
                return new BaseResponse<>(result);
            } catch (BaseException exception) {
                return new BaseResponse<>((exception.getStatus()));
            }
        }
    ```
    
- service
    
    ```java
    // 게시판 삭제 (PATCH)
        public void deleteBoard(PatchBoardReq patchBoardReq) throws BaseException {
            try {
                if(boardDao.isCheckedPwDelete(patchBoardReq.getIdx(),patchBoardReq.getPassword()) != 1) {
                    throw new BaseException(INCORRECT_PASSWORD);
                }
                int result = boardDao.deleteBoard(patchBoardReq);
                if (result == 0) {
                    throw new BaseException(DELETE_FAIL_BOARD);
                }
            } catch (NullPointerException exception) {
                throw new BaseException(DATABASE_ERROR);
            }
        }
    ```
    
- dao
    
    ```java
    public int deleteBoard(PatchBoardReq patchBoardReq) {
            String deleteBoardQuery = "update board set deleted = 'Y' where idx = ?";
            Object[] deleteBoardParam = new Object[]{patchBoardReq.getIdx()};
    
            return this.jdbcTemplate.update(deleteBoardQuery, deleteBoardParam);
        }
    
        public int isCheckedPwDelete(int idx, String password) {
            String getPasswordQuery = "select exists (select * from board where idx = ? AND password = ?)"; //해당 조건에 맞는 게시판이 있는지 확인, 있으면 1, 없으면 0 반환
            Object[] updateBoardParams = new Object[]{idx, password};
            return this.jdbcTemplate.queryForObject(getPasswordQuery, int.class, updateBoardParams);
        }
    ```
![게시판 삭제](https://user-images.githubusercontent.com/48826098/204151113-b3ec37da-d11b-4e1e-83bb-3392a78091c1.jpg)

![게시판 삭제 후](https://user-images.githubusercontent.com/48826098/204151112-84cc53ab-deaf-4264-a9f4-a0bcf2f63e77.jpg)
