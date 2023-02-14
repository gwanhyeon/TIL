# Optional 사용방법


> Optional 사용시 반환 처리 

```java
Optional<MobileCarrier> mobileCarriers = mobileCarrierRepository.findAll();

나쁜 예)

if(mobileCarriers.isPresent()){
    MobileCarrier mobileCarrier = mobileCarriers.get();
}

올바른 예)
MobileCarrier mobileCarriers = mobileCarriers.orElse(null);

```

isPresent() 함수로 조건 체크후 get()을 통하여 엔티티를 가져오는 것보다 orElse()를 통해서 처리하는것이 유효, 그 이유는 orElse는 Optional의 여부와 관계없이 실행후 값을 처리할 수 있음.

orElseGet(*): *는 Optional 값이 없을때만 전달된 람다식이 실행
orElseThrow(+): +는 Optional 값이 없을때 예외 발생

> 예외 처리 예제

```java
// bad
Optional<Member> member = ...;
if (member.isPresent()) {
    return member.get();
} else {
    return null;
}

// good
Optional<Member> member = ...;
return member.orElse(null);

// bad
Optional<Member> member = ...;
if (member.isPresent()) {
    return member.get();
} else {
    throw new NoSuchElementException();
}

// good
Optional<Member> member = ...;
return member.orElseThrow(() -> new NoSuchElementException())
```

> Optional로 감싸 반환된 null 객체보다는 비어있는 컬렉션을 반환하는게 더 좋음.

```java
// bad
public interface MemberRepository<Member, Long> extends JpaRepository {
    Optional<List<Member>> findAllByNameContaining(String part);
}

// bad
List<Member> members = team.getMembers();
return Optional.ofNullable(members);

// good
public interface MemberRepository<Member, Long> extends JpaRepository {
    List<Member> findAllByNameContaining(String part);  // null이 반환되지 않으므로 Optional 불필요
}

// good
List<Member> members = team.getMembers();
return members != null ? members : Collections.emptyList();

```

> of(), ofNullable 혼동 주의

`of(X)은` X가 null이 아님이 확실할 때만 사용해야 하며, X가 null이면 NullPointerException 이 발생한다.
`ofNullable(X)은` X가 null일 수도 있을 때만 사용해야 하며, X가 null이 아님이 확실하면 of(X)를 사용해야 한다.

> reference 

https://homoefficio.github.io/2019/10/03/Java-Optional-%EB%B0%94%EB%A5%B4%EA%B2%8C-%EC%93%B0%EA%B8%B0/