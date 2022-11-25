
## 해당 서비스에서 자주 사용되는 쿼리 10개 작성해보기</br>(예시: 회원가입, 내 피드 조회, 게시물 작성, 프로필 사진 수정, 게시물 삭제, 팔로잉하고 있는 유저 게시물 조회, 게시물 올린 시간 조회, 게시물 좋아요 개수 조회 등)




**작성할 쿼리**
- 회원가입
- 주소 등록
- 카테고리 리스트 조회
- 음식점 리스트 조회 
- 특정 카테고리의 음식점 조회
- 30분 이내 배달 가능 음식점 조회
- 리뷰 등록
- 특정 가게의 메뉴 리스트 조회
- 주문 내역 조회
- 쿠폰 조회


### 배달의 민족 ERD

![erd](https://user-images.githubusercontent.com/48826098/203914415-551144e7-3649-4429-bad8-f46b2468d1bb.png)


### SQL

▪️ 회원가입

```sql
INSERT INTO User(userId, userPw, nickName, email, userPhone, profile, grade, status) 
VALUES ('1', '1234', '김철수', 'A@naver.com', '010-1234-4567', NULL, 'vip', 'y');
```

![1  회원가입 결과](https://user-images.githubusercontent.com/48826098/203914490-326bb7a9-9d54-451b-ba4c-6f02f9433ca1.jpg)

▪️ 주소 등록

```sql
INSERT INTO UserAddress(userAddrId, userId, address, status) VALUES('1', '1', '경기도 용인시', 'D');
```

![2  주소 등록](https://user-images.githubusercontent.com/48826098/203914503-790440a6-e71c-4021-aa5b-79408bed24ec.jpg)

▪️ 카테고리 리스트 조회

```sql
SELECT categoryName From Category;
```

![3](https://user-images.githubusercontent.com/48826098/203914510-328d9526-9703-4ac1-8bdc-d5fd294718d5.jpg)

▪️ 주변 음식점 조회

```sql
SELECT storeName as 가게이름 , storeAddr as 주소 
FROM Store
WHERE storeAddr like '경기도 용인시%';
```

![화면 캡처 2022-11-03 031313](https://user-images.githubusercontent.com/48826098/203914645-f2c10e76-d399-4825-8efa-00cd40fc10a3.jpg)

▪️ 특정 카테고리의 음식점 조회

```sql
SELECT storeName
 FROM Store
 WHERE categoryId = 
 (SELECT categoryId
 FROM category
 WHERE categoryName = '분식');
```

![5](https://user-images.githubusercontent.com/48826098/203914522-3834e99a-76b5-41df-826c-4070c134480b.jpg)

▪️ 30분 이내 배달 가능 음식점 조회

```sql
SELECT storeName AS '30분 이내 배달 가능 음식점' FROM store WHERE deliveryTime <= 30;
```

![6](https://user-images.githubusercontent.com/48826098/203914527-2f9f6915-6c8c-4a20-a180-0a1178d940a7.jpg)

▪️ 리뷰 등록

```sql
//리뷰 등록
INSERT INTO review(reviewId, userId, storeId, menu, score, content, picture, status, writingDate)
 VALUES ('1','1','2','바질 치킨','4.5','존맛탱',null,'y','2022-11-02');

//가게에 업데이트
UPDATE Store s
		inner join Review r
        on s.storeId = r.storeId
 SET reviewCnt = reviewCnt + 1, avgScore = format(((avgScore * reviewCnt + score) / (reviewCnt + 1)),1)
 WHERE s.storeId = 2;
```

등록 전

![리뷰 등록 전](https://user-images.githubusercontent.com/48826098/203914618-6e8d9708-1a1b-4394-a13b-cea4a095c9f1.jpg)

등록 후

![review](https://user-images.githubusercontent.com/48826098/203914591-9758c4e0-9573-4877-9059-340226d174f7.jpg)

▪️ 특정 가게 메뉴 조회

```sql
SELECT menuName as '메뉴 이름', menuPicture as '사진', price as '가격', description as '설명' 
FROM menu
WHERE storeId = 2;
```

![menu](https://user-images.githubusercontent.com/48826098/203914583-a27a48f6-f551-4b48-ad6f-44a5669b2a7b.jpg)

▪️ 주문 내역 조회

```sql
SELECT CASE WHEN ifnull(menuName, '') = '' THEN '합계' ELSE menuName END AS 메뉴,
 sum(price * menuCnt) AS 가격 , sum(menuCnt) AS 개수
FROM (menu m INNER JOIN ordermenu o ON m.menuId = o.menuId) INNER JOIN userOrder u ON (u.userId = o.userId & u.orderId = o.orderId)
GROUP BY menuName WITH ROLLUP;
```

![화면 캡처 2022-11-03 030918](https://user-images.githubusercontent.com/48826098/203914630-ad770072-bddd-4e7b-a59a-26cbff63eb37.jpg)

▪️ 쿠폰 조회

```sql
SELECT couponName as '쿠폰 이름', minOrderPrice as '최소 주문 금액', discount as '할인율(%)', expired as '만료일'
FROM Coupon
WHERE userId = 1;
```

![coupon](https://user-images.githubusercontent.com/48826098/203914552-5a2136f6-0274-4987-abcd-ad23b2608e1f.jpg)
