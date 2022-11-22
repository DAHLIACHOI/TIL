- SQL 문법: DML의 **SELECT** 위주로 학습
    - DDL(Data Definition Language)
        - CREATE
            - 테이블을 생성하는 역할
            - 객체를 의미하는 것이므로 단수형으로 이름을 짓는걸 권고한다.
            - 유일한 이름으로 명명해야 한다.
            - 테이블 내의 컬럼명 또한 중복되지 않는 유일한 이름으로 명명해야 한다.
            - 정의할 때 각 칼럼은 `,`으로 구분하며 테이블 생성문의 마지막은 `;`이다.
            - 칼럼명은 데이터 표준화 관점에서 일관성 있게 사용해야 한다.
            - 칼럼 뒤에 데이터 유형을 반드시 지정해야 한다.
            - 테이블과 컬럼명은 반드시 문자로 시작한다.
            - 대소문자를 구분하지 않지만 기본적으로 대문자로 만들어진다.
        - ALTER
            - 테이블 구조를 수정하는 역할
        - DROP
            
            테이블을 삭제하는 역할
            
        - TRUNCATE
            
            테이블을 초기화하는 역할
            
    - **DML (Data Manipulation Language)**
        - INSERT
            - 테이블에 데이터를 추가하는 역할
        - **SELECT**
            - 데이터베이스에서 데이터를 검색하는 역할
            
            ▪️ 모든 칼럼을 보여줌
            
            ```sql
            select * from 테이블명(여기선 department라고 하겠음);
            ```
            
            ▪️ 특정 칼럼 검색
            
            ```sql
            select name, deptno from department;
            ```
            
            ▪️ SELECT 컬럼에 Alias부여하기 (별칭 부여)
            
            ```sql
            select name 부서명, deptno 부서번호 from department;
            
            of
            
            select name as 부서명, deptno as 부서번호 from department;
            ```
            
            ▪️ SELECT 칼럼의 합성 (Concatenation)
            
            ```sql
            select concat(empno, "-", deptno) as '사번-부서번호" from emplyee;
            
            -> 사번하고 부서 번호를 합치고, alias 부여
            ```
            
            ▪️ SELECT 중복행 제거
            
            ```sql
            select deptno from employee;
            -> deptno에 중복되는 값들 제거
            ```
            
            ▪️ SELECT 정렬
            
            - order by 사용
            
            → asc : 오름차순 정렬, 정의안해주면 자동으로 이거 사용
            
            → desc : 내림차순 정렬
            
            ```sql
            select empno, ame from employee order by name;
            -> 자동으로 오름차순 정렬
            
            select empno, name from employee order by name desc;
            -> 내림차순 정렬
            
            select empno, name from employee order by 2 desc;
            -> name을 기준으로 내림차순 정렬
            ```
            
            ▪️ SELECT 특정 행 검색 
            
            - WHERE절 사용
            
            ```sql
            SELECT(DISTINCT) 칼럼명(ALIAS) FROM 테이블명 WHERE 조건식 ORDER BY 칼럼이나 표현식 (ASC OR DESC);
            ```
            
            - 산술비교 연산자
            
            ```sql
            select name, hiredate from employee where hiredate < 1981;
            ```
            
            - 논리비교 연산자
            
            ```sql
            select name, deptno from employee where deptno=30;
            -> 부서번호가 30인 사원이름과 부서번호 출력
            ```
            
            - IN
            
            ```sql
            select name, deptno from employee where deptno in (10,20);
            -> 부서번호가 10또는 20인 사원이름과 부서번호 출력
            ```
            
            - AND
            
            ```sql
            select name, deptno, salary from employee where deptno = 10 and salary < 1500;
            ```
            
            - LIKE
            - 와일드 카드를 사용하여 특정 문자를 포함한 값에 대한 조건을 처리
            → `%`는 0에서부터 여러 개의 문자열을 나타낸다.
            → `_`는 단 하나의 문자를 나타내는 와일드 카드
            
            ```sql
            select * from employee where name like 'A%';
            -> A로 시작하는 이름을 가진 사원들 출력
            
            select * from employee where name like '%A';
            -> A로 이름이 끝나는 사원들 출력
            
            select * from employee where name like '%A%';
            -> 이름 안에 A가 들어가는 사원들 출력
            
            select * from employee where name like '_A%';
            -> 이름의 두 번째 스펠링이 'A'인 사원들 출력
            ```
            
            ▪️ SELECT 함수
            
            - `UPPER`, `UCASE`, `LOWER`, `LCASE` : 문자열을 대문자 혹은 소문자로 나타냄
            
            ```sql
            select lower(name) from employee;
            ```
            
            …
            
            나머지는 아래 블로그 참고
            
            [[데이터베이스] DML (SELECT)](https://velog.io/@re-deok/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-DML-SELECT)
            
        - UPDATE
            - 테이블 내에 존재하는 데이터를 수정하는 역할
        - DELETE
            - 테이블에서 데이터를 삭제하는 역할
    - DCL(Data Control Language)
        - GRANT
            - 특정 데이터베이스 사용자에게 특정 작업에 대한 수행권한 부여를 한다.
        - REVOKE
            
            특정 데이터베이스 사용자에게 특정 작업에 대한 권한을 박탈, 회수한다.
            
    - TCL
        - DCL과 비슷한 맥락이지만 데이터를 제어하는 언어가 아닌 트랜잭션을 제어할 때 사용한다.
        - 논리적인 작업 단위를 묶어 DML에 의해 조작된 결과를 트랜잭션 별로 제어한다.
        
        ⭐ 트랜잭션이란?
        
        > 데이터베이스의 상태를 변화시키기 위해 수행되는 작업의 단위를 말한다.
        보통 DBMS 성능을 초당 트랜잭션이 몇 개가 실행되었는지로 측정한다.
        MySQL의 입력하는 모든 명령어들은 각각 하나의 트랜잭션이라고 할 수 있다.
        > 
- SQL 참고자료들(thanks to 1기 선배님)
    - 루시(Lucy)
        - LENGTH
            
            [[MSSQL] 문자 숫자 정렬](https://kojin777.tistory.com/243)
            
        - LEFT
            
            [[MSSQL] 문자열 자르기 (LEFT,RIGHT,SUBSTRING) 사용법 & 예제](https://coding-factory.tistory.com/99)
            
        - SUBSTRING_INDEX
            
            [MySQL - 컬럼내 문자열 자르기 SUBSTRING_INDEX](https://whdrnr01.tistory.com/480)
            
    - 혜또(Hyeddo)
        1. COUNT , SUM 집계 함수
            - aggregate 함수
            - COUNT는 해당 attribute의 개수를, SUM은 해당 attribute의 합을 보여줌
            - SQL 에서 제공하는 5개의 기본 내장 집계 함수
                - **avg** : 평균
                - **min**: 최솟값
                - **max**: 최댓값
                - **sum**: 총합
                - **count**: 개수
            
            ```sql
            /* 2018 봄에 수업을 한 교수의 총 명 수 */
            SELECT **count**(distinct ID)
            FROM teaches
            WHERE semester="Spring" and year=2018;
            
            # 모든 course의 수
            SELECT count(*)
            FROM course;
            ```
            
        2. 문자형 함수
            - 문자형 함수는 문자 데이터를 매개 변수로 받아들여서 문자나 숫자 값의 결과를 돌려주는 함수
        3. where 절 조건
            - 연산자( (<, ≤, >, ≥, =, <>), (+,-,*,/))
            - 논리 접속사 (**and, or, not**)
                
                ```sql
                where dept_name = "Comp. Sci" and salary > 70000;
                ```
                
            - 범위 조건 (between and)
                - 예시: 급여가 90000과 100000 사이에 있는 교수의 이름 ($90,000\leq salary \leq 100,000$)
                    
                    ```sql
                    SELECT name
                    FROM instructor
                    WHERE salary **BETWEEN** 90000 **AND** 100000
                    ```
                    
            - is null
                
                ```sql
                
                WHERE salary IS NULL
                WHERE salary IS NOT NULL
                
                ```
                
            - like
                - SQL은 string-matching operator를 사용할 수 있음
                    
                    문자열의 값을 정확하게 모를 때, wild 카드를 써서 매치시키는 경우 많음
                    
                - **LIKE** 연산자 : 패턴 일치 수행 가능
                    - **percent (%)** : 어떤 부분 문자열과도 일치 (길이가 0 이상인 문자열과 매치)
                    - **underscore (_)** : 어떤 문자와도 일치 (1 캐릭터와 매치)
                - 예시
                    - 이름에 "dar"이 들어가는 instructor를 찾아라
                        
                        ```sql
                        SELECT name
                        FROM instructor
                        WHERE name **LIKE** '**%dar%**'
                        ```
                        
                    - string "100%"와 매치 → escape 사용
                        
                        ```sql
                        **LIKE** '100\%' **ESCAPE** '\'
                        ```
                        
                    - 'intro%': 'intro'로 시작하는 string
                    - '%Comp%': Comp를 substring으로 가진 string
                    - '_ _ _': 3 글자를 가진 string
                    - '_ _ _ %': 3글자 이상인 string
        4. 서브 쿼리
            - subquery: 다른 질의 안에 포함된 select-from-where
            - 어떻게?
                - From 절에서: sfw 결과로 table 나옴
                - Where 절에서: **B <operation> (subquery)** (B: column)
                - Select 절에서: single 값을 반환하는 subquery로 대체 가능
            - 예시: Set Membership
                - 어떤 원소가 집합의 멤버냐? 아니냐?
                    - $\in$ : **in**
                    - $**\notin$ : not in**
                - 예: 2018 봄과 2017 가을에 열린 강의를 찾자
                    - Set Membership
                    
                    ```sql
                    SELECT DISTINCT course_id
                    FROM section
                    WHERE semester="Fall" and year=2017 and
                    			course_id **IN** (SELECT course_id
                    										FROM section
                    										WHERE semester="Spring" and year=2018);
                    ```
                    
                    - Intersection
                    
                    ```sql
                    (SELECT course_id FROM section WHERE sem="Fall" AND year=2017)
                    **INTERSECTION**
                    (SELECT course_id FROM section WHERE sem="Spring" AND year=2018)
                    ```
                    
        5. 반올림, 버림 함수
            - 반올림 함수
                
                ROUND(숫자, m)
                
                - m이 양수일 경우 : 반올림하여 소수점 m자리까지 보이게
                - m이 생략될 경우 : 반올림하여 소수점이 안 보이게
                - m이 음수일 경우 : m자리에서 반올림
            - 버림 함수
                
                TRUNC(숫자, m)
                
                - m이 양수일 경우 : 소수점 m자리까지 보이게. 나머지는 버림
                - m이 생략될 경우 : 소수점이 안 보이게. 나머지는 버림
                - m이 음수일 경우 : m자리에서 버림
        6. Group By
            
            특정 컬럼을 그룹화 하는 **GROUP BY**
            
            특정 컬럼을 그룹화한 결과에 조건을 거는 **HAVING**
            
            - SELECT 컬럼 FROM 테이블 [WHERE 조건식]
            GROUP BY 그룹화할 컬럼 [HAVING 조건식] ORDER BY 컬럼1 [, 컬럼2, 컬럼3 ...];
        7. is, null, is not null
            
            IS NULL 은 입력값을 확인하여 NULL이면 TRUE를, NULL이 아니면 FALSE를 리턴.
            
            IS NOT NULL 은 IS NULL과는 반대로 입력값이 NULL이면 FALSE를, NULL이 아니면 TRUE를 리턴.
            
            - WHERE [컬럼명] IS NULL
            - WHERE [컬럼명] IS NOT NULL
        8. JOIN (InnerJoin / Left Join / Right Join / OuterJoin / Full Join )
            
            
            **1. INNER JOIN : 내부조인 ->교집합**
            
            **2. LEFT/RIGHT JOIN -> 부분집합**
            
            **3. OUTER JOIN : 외부조인 ->합집합**
            
    - 케빈
        
        🧐 **추가적으로 알아보면 좋을 SQL 함수**
        
        1. COUNT , SUM 집계 함수
            
            COUNT 함수는 컬럼내 레코드의 개수를 세주는 함수
            
            SUM 함수는 컬럼 내 레코드 값의 총합(자료형이 숫자만 가능)
            
        2. 문자형 함수
            
            
        3. where 절 조건: WHERE 조건 1 AND 조건2, 조건1 OR 조건2, NOT 조건 like '문자'(열)' mysql은 대소문자 구분 x
        4. 서브 쿼리 : **쿼리 안에 있는 쿼리. WHERE 절/FROM 절/SELECT 절 안에 들어가는 쿼리를 통칭하여 서브쿼리** 
        
        ```
        SELECT storeName
        FROM Store A
        WHERE A.categoryIdx IN (SELECT categoryIdx
                                FROM Category C
                                WHERE C.categoryName = '1인분');
        
        # 카테고리에서 카테고리 네임이 1인분인 카테고리idx를 a에서 찾아 storename을 찾음.
        ```
        
        1. 반올림, 버림 함수: CEIL (반올림 함수), FLOOR(내림 함수), **ROUND(n,반올림할 위치), TRUNC(n, 버림할 위치)**
        2. Group By : 특정 컬럼을 그룹화 하는 **GROUP BY,** 특정 컬럼을 그룹화한 결과에 조건을 거는 **HAVING**
        
        [[MySQL] 그룹화하여 데이터 조회 (GROUP BY)](https://extbrain.tistory.com/56)
        
        1. is, null, is not null: IS NULL: 컬럼값이 NULL인 값 불러오기
            
            IS NOT NULL : 컬럼값이 NULL이 아닌 값 불러오기
            
        2. JOIN (InnerJoin / Left Join / Right Join / OuterJoin / Full Join )
        
        INNER JOIN : 여러 테이블간의 조건을 만족하는 행을 반환할때 사용 (두 테이블의 교집합)
        
        SELECT *
        
        FROM TABLE1 T1
        
        INNER JOIN TABLE2 T2
        
        ON(T1.key = T2.key)
        
        
        OUTER JOIN : 2개 이상의 테이블이 조인될 때 어느 한쪽 테이블엔 데이터가 존재하는데 / 다른 쪽 테이블에는 데이터가 존재하지 않는 경우를 해결하기 위한 조인기법
        
        A,B 테이블 JOIN 할 경우, 조건에 맞지 않는 데이터 표시
        
        ON 대신 USING 조건(공통되는 컬럼명)절도 사용 가능
        
        LEFT JOIN : 두 개의 테이블에서 같은 것을 조회하고 왼쪽 테이블에 있는 것은 모두 포함해서 조회하는 것을 LEFT OUTER JOIN
        
        SELECT 
        
        FROM A LEFT OUTER JOIN B ON ()
        
        RIGHT JOIN : 두개의 테이블에서 같은 것을 조회하고 오른쪽 테이블에 있는 것은 모두 포함해서 조회 하는 것(LEFT 반대)
        
        SELECT
        
        FROM A RIGHT OUTER JOIN B ON ()
        
        FULL JOIN: 양쪽 테이블에 있는 데이터를 모두 보여줌( 합집합)
        
        
    - 케융
        1. 집계 함수_COUNT, SUM, AVG, MAX, MIN
            - [https://sejinworld.tistory.com/31](https://sejinworld.tistory.com/31)
        2. 문자형 함수
            - [https://moonpiechoi.tistory.com/102](https://moonpiechoi.tistory.com/102) 깔끔하게 표로 정리되어있음!
            - [https://data-make.tistory.com/6](https://data-make.tistory.com/6) 위에 없는 함수도 좀 있고, 엄청 자세하게 설명!
        3. where 절에서 사용하는 조건들
            - [https://goldsony.tistory.com/97](https://goldsony.tistory.com/97) 
            _연산자, AND/OR, BETWEEN-AND, IS (NOT)NULL, IN, EXITS, LIKE
            - NOT 도 있음! 
            ex) WHERE NOT a=5;  (a(칼럼명)=5 가 아닌~) 
                  // WHERE userID NOT IN ('user1', 'user3'); (userID가 user1과 user3인 데이터를 제외하고   ~)
        4. 서브 쿼리
            - [https://mozi.tistory.com/233](https://mozi.tistory.com/233) 설명+예시도 있는데, 예문에 대한 결과값은 없음ㅠ
        5. 반올림, 버림 함수
            - [https://omnia-omnibus.tistory.com/4](https://omnia-omnibus.tistory.com/4) 반올림/버림/올림/내림 함수
        6. Group By
            - [https://extbrain.tistory.com/56](https://extbrain.tistory.com/56) GROUP BY로 데이터 조회하기
        7. is null, is not null
            - [https://araikuma.tistory.com/503](https://araikuma.tistory.com/503) IS NULL / IS NOT NULL 인 데이터 조회하기
        8. JOIN (InnerJoin / Left Join / Right Join / OuterJoin / Full Join )
            - [https://pearlluck.tistory.com/46](https://pearlluck.tistory.com/46) _벤다이어그램 설명
            - [https://gent.tistory.com/376](https://gent.tistory.com/376) _실행예시 설명
        9. Limit (함수는 아닌 듯! 키워드?)
            
            
        
    - 제로
        1. COUNT , SUM 집계 함수
        2. 문자형 함수 ⏩ [참고](https://blog.naver.com/xotjd7184/222288348416)
        3. where 절 조건
        4. 서브 쿼리 ⏩ [참고](https://blog.naver.com/dktmrorl/222304577464)
        5. 반올림, 버림 함수
        6. Group By ⏩ [참고](https://blog.naver.com/tommybee/222464668290), [참고2](https://blog.naver.com/2206017/222433493826)
        7. is, null, is not null
        8. JOIN (InnerJoin / Left Join / Right Join / OuterJoin / Full Join )
        
        [나만의공간。 : 네이버 블로그](https://blog.naver.com/writer0713/222277142471)
        
        [♬수박의 맛있는 블로그♬ : 네이버 블로그](https://blog.naver.com/supark_subin0209/222525485287)
        
        [혜온의 블로그:) : 네이버 블로그](https://blog.naver.com/jhwon0616/222510118638)
        
        ---
        
    - 인하대 서버 2팀
        - COUNT , SUM 집계 함수
            
             **COUNT**
            
            ```sql
            SELECT COUNT(*) FROM (테이블명);
            ```
            
            ㄴ 테이블에 있는 모든 레코드의 수를 출력한다.
            
            **SUM**
            
            ```sql
            SELECT SUM(필드명) FROM (테이블명);
            ```
            
            ㄴ 필드의 합계를 출력한다.
            
            **MAX & MIN**
            
            ```sql
            SELECT name, max(필드명) FROM (테이블명);
            ```
            
            ㄴ 필드의 최대값/최소값을 출력한다.
            
            **AVG**
            
            ```sql
            SELECT AVG(필드명) FROM (테이블명);
            ```
            
            ㄴ 필드의 평균을 출력한다.
            
        - 문자형 함수
            
            : 문자 데이터를 매개 변수로 문자나 숫자값의 결과를 돌려주는 함수
                        
        - where 절 조건
            
            where 절 : 테이블에서 특정 조건에 부합하는 데이터만 조회하고 싶을 때 사용
            
            ex)
            
            **조건을 충족하는 데이터 조회**
            
            ```sql
            SELECT * FROM employee
            WHERE job='사원';
            ```
            
            **특정 값 이상인 데이터 조회**
            
            ```sql
            SELECT * FROM employee
            WHERE salary>=500;
            ```
            
            **논리연산자 AND/OR 사용**
            
            ```sql
            SELECT * FROM employee
            WHERE job!='사장'
            AND salary>=500;
            ```
            
            **BETWEEN A AND B**
            
            ```sql
            SELECT * FROM employee
            WHERE salary BETWEEN 300 AND 500;
            ```
            
            **IN**
            
            ```sql
            SELECT * FROM employee
            WHERE salary IN (300,400,500,600);
            ```
            
        - 서브 쿼리
            
            : 하나의 SQL 문에 포함되어 있는 또 다른 SQL문
            
            - 사용 시 주의사항
                - 서브쿼리를 괄호로 감싸서 사용한다.
                - 서브쿼리는 단일 행 또는 복수 행 비교 연산자와 함께 사용 가능하다.
                - 서브쿼리에서는 ORDER BY를 사용하지 못ㅎㄴ다.
            1. SELECT 절에서의 서브쿼리 : 서브쿼리의 결과 값은 **하나만 출력**되어야 한다.
            
            ```sql
            SELECT CD_PLANT, NM_PLANT
            (SELECT AVG(UM) FROM TABLE_ITEM) AS UM
            FROM TABLE_PLANT
            ```
            
            1. From 절에서의 서브쿼리: 서브쿼리에서 **조회된 값을 테이블처럼 활용**
            
            ```sql
            SELECT CD_PLANT, NM_PLANT, AM
            FROM (SELECT * FROM TABLE_PLANT)
            ```
            
            1. Where 절에서의 서브쿼리
            
            ```sql
            SELECT CD_PLANT
            FROM TABLE_PLANT
            WHERE CD_PLANT IN(SELECT CD_PLANT FROM TABLE_PLANT WHERERE PLANT='1000' AND COMPANY='0327')
            ```
            
        - 반올림, 버림 함수
            - 반올림 함수
                - ROUND()를 사용
                
                ```sql
                SELECT ROUND(3456.789) FROM DUAL; // 3456
                SELECT ROUND(3456.789,1) FROM DUAL; // 3456.8
                SELECT ROUND(3456.789,2) FROM DUAL; // 3456.80
                
                SELECT ROUND(3456.789, -1) FROM DUAL; // 3460
                SELECT ROUND(3456.789,-2) FROM DUAL; // 3500
                ```
                
            - 버림 함수
                - TRUNC()를 이용
                
                ```sql
                SELECT TRUNC(3456.1234567) FROM DUAL; // 3456
                SELECT TRUNC(3456.1234567,1) FROM DUAL; // 3456.1
                SELECT TRUNC(3456.1234567,4) FROM DUAL; // 3456.1234
                SELECT TRUNC(3456.1234567,-1) FROM DUAL; //3450
                SELECT TRUNC(3456.1234567,-2) FROM DUAL; //3400
                ```
                
        - Group By
            
            : 집계함수의 결과를 특정 컬럼을 기준으로 묶어 결과를 출력해주는 쿼리이다.
            
            - 형식
                
                ```sql
                SELECT column, 집계함수(column)
                FROM TABLE
                (WHERE column=data)
                GROUP BY column;
                ```
                
            - 예제
                
                citykorea 테이블의 도시별 인구 합계를 출력하시오.
                
                ```sql
                SELECT district, sum(population)
                FROM citykorea;
                GROUP BY district;
                ```
                
        - is null, is not null
            - is null
                
                : 필드 값이 비어 있는 경우
                
                ```sql
                SELECT (필드명)
                FROM (테이블명)
                WHERE (필드명) IS NULL
                ```
                
            - is not null
                
                : 필드 값이 비어 있지 않은 경우
                
                ```sql
                SELECT (필드명)
                FROM (테이블명)
                WHERE (필드명) IS NOT NULL
                ```
                
        - JOIN (InnerJoin / Left Join / Right Join / OuterJoin / Full Join )
            
            : 둘 이상의 테이블을 연결해서 데이터를 검색한ㄴ 방법
            
            연결하려면 테이블들이 적어도 하나의 컬럼을 공유하고 있어야함 → PK 또는 FK 값을 사용
            
            
            - Inner JOIN
                
                : 교집합, 공통적인 부분만 SELECT 됨
                                
                
                ➡ ID가 공통인 행들만 SELECT됨
                
                ```sql
                SELECT A.ID, A.ENAME, A.KNAME
                FROM A INNER JOIN B
                ON A.ID=B.ID;
                ```
                
            - Left Join
                
                : 1) 조인 기준 **왼쪽에 있는거 '다'** SELECT됨 (공통적인 부분+LEFT)
                
                
                ```sql
                SELECT A.ID, A.ENAME, A.KNAME
                FROM A LEFT OUTER JOIN B
                ON A.ID=B.ID;
                ```
                
                : 2) 조인 기준 **왼쪽에 있는거'만'** SELECT됨 (공통적인 부분+LEFT)
                
                
                ```sql
                SELECT A.ID, A.ENAME, A.KNAME
                FROM A LEFT OUTER JOIN B
                ON A.ID=B.ID
                WHERE B.ID IS NULL;
                ```
                
            - Right Join
                
                : 1) 조인 기준 **오른쪽에 있는거 '다'** SELECT됨
                
                
                ```sql
                SELECT A.ID, A.ENAME, A.KNAME
                FROM A RIGHT OUTER JOIN B
                ON A.ID=B.ID;
                ```
                
                : 2) 조인 기준 **오른쪽에 있는거만** SELECT됨 
                
                
                ```sql
                SELECT A.ID, A.ENAME, A.KNAME
                FROM A RIGHT OUTER JOIN B
                ON A.ID=B.ID
                WHERE A.ID IS NULL;
                ```
                
            - Outer Join
                
                : 1) A 테이블이 가지고 있는거, B 테이블이 가지고 있는거 둘 다 SELECT
                
                
                ```sql
                SELECT A.ID, A.ENAME, A.KNAME
                FROM A FULL OUTER JOIN B
                ON A.ID = B.ID
                ```
                
                : 2) 교집합을 제외하고 SELECT
                
                
                ```sql
                SELECT A.ID, A.ENAME, A.KNAME
                FROM A FULL OUTER JOIN B
                ON A.ID = B.ID
                WHERE A.ID IS NULL OR B.ID IS NULL;
                ```
                
            - Full Join
                
                
            
            
- [선택] ORM(Object Relational Mapping)
    - ORM이란?
        - ORM(Object-Relational Mapping)은 이름 그대로 객체와 관계형 데이터베이스를 매핑한다는 뜻이다.
        - ORM 프레임워크는 객체와 테이블을 매핑해서 패러다임의 불일치 문제를 개발자 대신에 해결해준다.
        
        
        ``` 
        예를 들면 ORM 프레임워크를 사용하면 객체를 데이터베이스에 저장할 때 INSERT SQL을 직접 작성하는 것이 아니라 객체를 마치 자바 컬렉션에 저장하듯이 ORM프레임워크에 저장하면 된다.
        그러면 ORM 프레임워크가 적절한 INSERT SQL을 생성해서 데이터베이스에 객체를 저장해준다.
        
        [JPA 이용해서 객체 조회]
        Member member = jpa.find(memberId);
        
        ```
        
        - ORM 프레임워크는 단순히 SQL을 개발자 대신 생성해서 데이터베이스에 전달해주는 것뿐만 아니라 다양한 패러다임의 불일치 문제들도 해결해준다. (상속이 있는 경우 테이블을 조인하고 그 테이블에서 또 해당되는 객체를 생성해야되면 SQL 코드양이 엄청 많아져서 그걸 그냥 JPA에서 한번에 해주는거!)
        - 따라서 객체 측면에서는 정교한 객체 모델링을 할 수 있고 관계형 데이터베이스는 데이터베이스에 맞도록 모델링하면 된다.
    - ORM의 등장배경
        - 객체지향 프로그래밍
        - 관계형 데이터베이스
        - 객체지향 프로그래밍과 관계형 데이터베이스의 불일치
    - JPA
        - JAVA 진영의 ORM 기술 표준이다.
        - JPA는 애플리케이션과 JDBC사이에서 동작 ← JDBC란 자바에서 데이터 베이스에 접속할 수 있도록 하는 자바 API (데이터베이스에서 자료를 쿼리하거나 업데이트하는 방법을 제공)
        - JPA덕분에 특정 구현 기술에 대한 의존도를 높을 수 있고 다른 구현 기술로 손쉽게 이동할 수 있는 장점이 있음
        - JPA 버전 역사..?
            - JPA 1.0 → 초기 버전. 복합 키와 연관관계의 기능 부족
            - JPA 2.0 → 대부분의 ORM기능 포함. JPA Critieria 추가
            - JPA 2.1 → 스토어드 프로시저 접근 . 컨버터, 엔티티 그래프 추가
        - JPA 사용 이유
            - 생산성
            - 유지보수
            - 패러다임 불일치 해결
            - 상속, 연관관계, 객체 그래프 탐색, 비교하기와 같은 패러다임 문제
            - 성능
    - TypeORM
        - Node.js, Browser, React Native 플랫폼 등에서 js, ts와 함께 사용할 수 있는 orm이다. → JPA는 JAVA ORM이고, TypeORM은 JS ORM이라는거!
        - MySQL, PostgreSQL, MariaDB, MS SQL Server, Oracle, WebSQL 데이터베이스 지원