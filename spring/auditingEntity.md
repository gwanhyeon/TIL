# auditingEntity의 의미

 AuditingEntityListener을 사용하기 위해선 어플리케이션 구동 클래스에  @EnableJpaAuditing을 사용한다. 

```java
@SpringBootApplication
@EnableJpaAuditing
public class JpaTestApplication {
    public static void main(String[] args) {
        SpringApplication.run(JpaTestApplication.class, args);
    }
}
```

엔티티에서 @EntityListener( value = AuditingEntityListener.class) 를 지정하면 사용할 수 있다. 
어노테이션으로 @CreatedBy(작성자), @CreatedDate(작성일) @LastModifiedDate(수정일), @LastModifiedBy(수정자)을 자동으로 넣어 주는 기능을  제공한다 .  
```java
@Data
@NoArgsConstructor
@AllArgsConstructor
@Entity
@EntityListeners(AuditingEntityListener.class)
public class Book implements Auditable2 {

    @Id @GeneratedValue
    private Long id;

    private String name;

    private String author;

    @CreatedDate
    private LocalDateTime createdAt;

    @LastModifiedDate
    private LocalDateTime updatedAt;
    
}
```

# baseEntity 사용하기 

```java
import com.ugo.jpatest.domain.entitylistener.Auditable2;
import lombok.Data;
import org.springframework.data.annotation.CreatedDate;
import org.springframework.data.annotation.LastModifiedDate;
import org.springframework.data.jpa.domain.support.AuditingEntityListener;

import javax.persistence.EntityListeners;
import javax.persistence.MappedSuperclass;
import java.time.LocalDateTime;

@EntityListeners(value = {AuditingEntityListener.class})
@MappedSuperclass
@Data
public class BaseEntity implements Auditable2 {

    @CreatedDate
    private LocalDateTime createdAt;

    @LastModifiedDate
    private LocalDateTime updatedAt;

}
```
생성 시간과 수정시간을 저장하는 엔티티이다 해당 필드는 모든 엔티티에 적용될 것이기 때문에 다른 클래스에서 상속받아서 사용하는 BaseEntity 가 된다 baseEntity 임을 알리기 위해선 @MappedSuperClass를 붙혀줘야한다. 해당 클래스를 상속받는 엔티티에서 해당 클래스 필드를 컬럼으로 사용하게 한다
