## 👉 H2 사용

```java
@Entity
// @Table(name = "") -> 테이블 이름이 다르다면 이렇게 직접 테이블명 적어줌
public class Member {

    @Id //pk 알려줘야됨!
    private Long id;
    // @Column(name = "") -> 컬럼 이름 다르면 이렇게 직접 선언해서 매핑 가능
    private String name;

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```
> 멤버 객체를 만들어주고, @Entity어노테이션으로 엔티티랑 DB 매핑


### 회원 등록

```java
import javax.persistence.EntityManager;
import javax.persistence.EntityManagerFactory;
import javax.persistence.EntityTransaction;
import javax.persistence.Persistence;
import java.util.List;

public class JpaMain {
    public static void main(String[] args) {
        EntityManagerFactory emf = Persistence.createEntityManagerFactory("hello"); // DB연결이나 웬만한건 다 해줌

        EntityManager em = emf.createEntityManager();

        EntityTransaction tx = em.getTransaction();
        tx.begin(); //db 트랜잭션 시작 . 데이터의 모든 변경은 트랜젝션에서 일어남

        try {
            // 등록
            Member member = new Member();

            member.setId(1L);
            member.setName("HelloA");
            em.persist(member);

            tx.commit(); // 커밋 꼭 하기
        } catch (Exception e) {
            tx.rollback();
        }finally {
            em.close(); // 끝내면 꼭 entity manager 닫아주고
        }
        emf.close(); // 모두 끝나면 factory manager 닫아줘야됨
    }
}

```

> **Manager Factory, entity manager 선언해줌**
> **데이터의 모든 변경은 트랜잭션에서 일어나기 때문에 꼭 트랜젝션 시작해주고, 성공적으로 하면 커밋, 실패하면 롤백**
> **멤버는 그냥 set사용해서 저장해주고 나서 persist 사용하면 됨**




### 회원 수정
```java
Member findMember = em.find(Member.class, 1L); // pk로 찾아줌
findMember.setName("HelloJPA");
```

> **find사용해서 pk를 통해서 해당 값에 맞는 거 찾아줌.
> 그러고 set사용해서 수정 가능**




### 회원 삭제

```java
Member findMember = em.find(Member.class, 1L)
em.remove(findMember);
```

> **해당 pk를 찾아 준 다음에 그 객체 remove사용해서 지움**




## JPQL
👉 가장 단순한 조회 방법이다. -> 약간 SQL 문법이랑 비슷!!
👉 근데 쿼리를 짤 때 SQL은 데이터베이스 테이블 대상으로 쿼리를 짠다면 JPQL은 엔티티 객체를 대상으로 쿼리를 짬

### 회원 조회

```java

List<Member> result = em.createQuery("select m from Member as m", Member.class)
                    .getResultList();

            for (Member member : result) {
                System.out.println("member.name = " + member.getName());
            }
```

> 회원 이름 조회하는 거임


➕ 몇번째 칼럼부터 몇개 조회하라고 사용하고 싶을 때

```java
List<Member> result = em.createQuery("select m from Member as m", Member.class)
                    .getResultList()
                    .setFirstResult(3)
                    .setMaxResult(8) ;
```

> 3번째 부터 8개 가져오라는 뜻임!!
