# JPA 영속성 컨텍스트

영속성 컨텍스트란 논리적인 개념(무형성)으로 엔티티를 영구 저장하는 환경이라고 할 수 있습니다. 특히, JPA를 이해하는데 가장 중요한 용어입니다. 그리고 EntityManager를 통하여 영속성 컨텍스트에 접근할 수 있습니다.

```

EntityManager.persist(entity);

```

다음과 같이 EntityManagerFactory가 생성시킨 EntityManager를 사용하여 Connection pool에 접근하여 Database에 접근할 수 있습니다.


# 비영속(new/transient)



```

Member member = new Member();
member.setId("memberId1");
member.setUsername("gwanhyeonkim")


```

# 영속(managed)


```

Member member = new Member();
member.setId("memberId1");
member.setUsername("gwanhyeonkim")

EntityManager em = emf.createEntityManager();
em.getTransaction().begin();
em.persist(member);

```

1. 엔티티 매니저 팩토리로 엔티티 매니저를 생성합니다.
2. 트랙잭션위에서 동작합니다.
3. 객체를 저장한 상태(영속) - 영속상태가 되는것 DB에 저장되는 상태가 아니며 트랜잭션 커밋시점에 해당 DB에 들어가게 됩니다.
4. 만약 1차캐시가 있다면 1차캐시를 사용합니다.

# 준영속(detached)

```
em.detach(member);

```

엔티티를 영속성 컨텍스트에서 분리시키고 준영속상태로 만듭니다.

# 삭제(removed)
```
em.remove(member);
```

# 영속성 컨텍스트 특징

1. 1차캐시를 활용합니다.
2. 동일성(Identity)를 보장합니다.
3. 트랜잭션을 지원하는 쓰기 지연을 일으킵니다(Transcational write-behind)
3. 변경 감지(Dirty Checking)이 가능합니다.
4. 지연 로딩(Lazy Loading)을 지원합니다

즉, 영속성 컨텍스트는 버퍼링과 캐싱의 기능을 가질 수 있습니다.
