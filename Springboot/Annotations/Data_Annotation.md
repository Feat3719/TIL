## Data Annotation
### @EnableJpaAuditing
> 감사(Auditing) 기능을 활성화 한다. Entity 의 생성일자(@CreatedDate), 마지막 수정일자(@LastModifiedDate)를 자동으로 관리 할 수 있다.

- 보통 Application 에 작성하여 적용한다.
<br>  

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.data.jpa.repository.config.EnableJpaAuditing;

@EnableJpaAuditing // Application 에 작성하여 적용한다.
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```
<br><br>

### @CreatedDate
> Entity 의 생성 시간을 자동으로 관리하기 위해 사용한다.

- Entity 가 생성되어 저장될 때의 시간이 해당 필드에 자동으로 할당된다.

<br><br>

### @LastModifiedDate
> Entity 의 마지막 수정 시간을 자동으로 관리한다.

- Entity 가 업데이트될 때마다 해당 필드에 현재 시간이 자동으로 할당된다.

<br><br>



```java
import jakarta.persistence.*;
import lombok.AccessLevel;
import lombok.Builder;
import lombok.Getter;
import lombok.NoArgsConstructor;
import org.springframework.data.annotation.CreatedDate;
import org.springframework.data.annotation.LastModifiedDate;

import java.time.LocalDateTime;

@Entity
@Getter
@NoArgsConstructor(access = AccessLevel.PROTECTED)
public class Article {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id", updatable = false)
    private Long id;

    @Column(name= "title", nullable = false)
    private String title;

    @Column(name = "content", nullable = false)
    private String content;

    @CreatedDate
    @Column(name = "created_at")
    private LocalDateTime createdAt;

    @LastModifiedDate
    @Column(name = "updated_at")
    private LocalDateTime updatedAt;

    @Builder
    public Article(String title, String content) {
        this.title = title;
        this.content = content;
    }

    public void update(String title, String content) {
        this.title = title;
        this.content = content;
    }
}

```
<br><br>