## ๐ H2 ์ฌ์ฉ

```java
@Entity
// @Table(name = "") -> ํ์ด๋ธ ์ด๋ฆ์ด ๋ค๋ฅด๋ค๋ฉด ์ด๋ ๊ฒ ์ง์  ํ์ด๋ธ๋ช ์ ์ด์ค
public class Member {

    @Id //pk ์๋ ค์ค์ผ๋จ!
    private Long id;
    // @Column(name = "") -> ์ปฌ๋ผ ์ด๋ฆ ๋ค๋ฅด๋ฉด ์ด๋ ๊ฒ ์ง์  ์ ์ธํด์ ๋งคํ ๊ฐ๋ฅ
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
> ๋ฉค๋ฒ ๊ฐ์ฒด๋ฅผ ๋ง๋ค์ด์ฃผ๊ณ , @Entity์ด๋ธํ์ด์์ผ๋ก ์ํฐํฐ๋ DB ๋งคํ


### ํ์ ๋ฑ๋ก

```java
import javax.persistence.EntityManager;
import javax.persistence.EntityManagerFactory;
import javax.persistence.EntityTransaction;
import javax.persistence.Persistence;
import java.util.List;

public class JpaMain {
    public static void main(String[] args) {
        EntityManagerFactory emf = Persistence.createEntityManagerFactory("hello"); // DB์ฐ๊ฒฐ์ด๋ ์ฌ๋งํ๊ฑด ๋ค ํด์ค

        EntityManager em = emf.createEntityManager();

        EntityTransaction tx = em.getTransaction();
        tx.begin(); //db ํธ๋์ญ์ ์์ . ๋ฐ์ดํฐ์ ๋ชจ๋  ๋ณ๊ฒฝ์ ํธ๋์ ์์์ ์ผ์ด๋จ

        try {
            // ๋ฑ๋ก
            Member member = new Member();

            member.setId(1L);
            member.setName("HelloA");
            em.persist(member);

            tx.commit(); // ์ปค๋ฐ ๊ผญ ํ๊ธฐ
        } catch (Exception e) {
            tx.rollback();
        }finally {
            em.close(); // ๋๋ด๋ฉด ๊ผญ entity manager ๋ซ์์ฃผ๊ณ 
        }
        emf.close(); // ๋ชจ๋ ๋๋๋ฉด factory manager ๋ซ์์ค์ผ๋จ
    }
}

```

> **Manager Factory, entity manager ์ ์ธํด์ค**
> **๋ฐ์ดํฐ์ ๋ชจ๋  ๋ณ๊ฒฝ์ ํธ๋์ญ์์์ ์ผ์ด๋๊ธฐ ๋๋ฌธ์ ๊ผญ ํธ๋์ ์ ์์ํด์ฃผ๊ณ , ์ฑ๊ณต์ ์ผ๋ก ํ๋ฉด ์ปค๋ฐ, ์คํจํ๋ฉด ๋กค๋ฐฑ**
> **๋ฉค๋ฒ๋ ๊ทธ๋ฅ set์ฌ์ฉํด์ ์ ์ฅํด์ฃผ๊ณ  ๋์ persist ์ฌ์ฉํ๋ฉด ๋จ**




### ํ์ ์์ 
```java
Member findMember = em.find(Member.class, 1L); // pk๋ก ์ฐพ์์ค
findMember.setName("HelloJPA");
```

> **find์ฌ์ฉํด์ pk๋ฅผ ํตํด์ ํด๋น ๊ฐ์ ๋ง๋ ๊ฑฐ ์ฐพ์์ค.
> ๊ทธ๋ฌ๊ณ  set์ฌ์ฉํด์ ์์  ๊ฐ๋ฅ**




### ํ์ ์ญ์ 

```java
Member findMember = em.find(Member.class, 1L)
em.remove(findMember);
```

> **ํด๋น pk๋ฅผ ์ฐพ์ ์ค ๋ค์์ ๊ทธ ๊ฐ์ฒด remove์ฌ์ฉํด์ ์ง์**




## JPQL
๐ ๊ฐ์ฅ ๋จ์ํ ์กฐํ ๋ฐฉ๋ฒ์ด๋ค. -> ์ฝ๊ฐ SQL ๋ฌธ๋ฒ์ด๋ ๋น์ท!!
๐ ๊ทผ๋ฐ ์ฟผ๋ฆฌ๋ฅผ ์งค ๋ SQL์ ๋ฐ์ดํฐ๋ฒ ์ด์ค ํ์ด๋ธ ๋์์ผ๋ก ์ฟผ๋ฆฌ๋ฅผ ์ง ๋ค๋ฉด JPQL์ ์ํฐํฐ ๊ฐ์ฒด๋ฅผ ๋์์ผ๋ก ์ฟผ๋ฆฌ๋ฅผ ์งฌ

### ํ์ ์กฐํ

```java

List<Member> result = em.createQuery("select m from Member as m", Member.class)
                    .getResultList();

            for (Member member : result) {
                System.out.println("member.name = " + member.getName());
            }
```

> ํ์ ์ด๋ฆ ์กฐํํ๋ ๊ฑฐ์


โ ๋ช๋ฒ์งธ ์นผ๋ผ๋ถํฐ ๋ช๊ฐ ์กฐํํ๋ผ๊ณ  ์ฌ์ฉํ๊ณ  ์ถ์ ๋

```java
List<Member> result = em.createQuery("select m from Member as m", Member.class)
                    .getResultList()
                    .setFirstResult(3)
                    .setMaxResult(8) ;
```

> 3๋ฒ์งธ ๋ถํฐ 8๊ฐ ๊ฐ์ ธ์ค๋ผ๋ ๋ป์!!
