## Jakarta Annotation
### @Transactional
> 트랜잭션을 적용하는 어노테이션.

❓트랜잭션이란  
데이터베이스의 데이터를 바꾸기 위해 묶은 작업의 단위

🗒️Example  
계좌 이체할때 A 계좌에서 출금 => B 계좌에 입금 과정 중에 A 계좌에서 출금을 성공하고 B계좌에서 입금을 진행하는 도중 실패 할 경우 심각한 상황이 벌어지므로  
이러한 과정을 한 작업의 단위로 묶어서 처리한다.  


```java
@Service
public class AccountService {

    @Autowired
    private AccountRepository accountRepository;

    @Transactional // 예시 
    public void transferMoney(Long fromAccountId, Long toAccountId, BigDecimal amount) {
        Account fromAccount = accountRepository.findById(fromAccountId).orElseThrow(...);
        Account toAccount = accountRepository.findById(toAccountId).orElseThrow(...);

        fromAccount.debit(amount);
        toAccount.credit(amount);

        accountRepository.save(fromAccount);
        accountRepository.save(toAccount);
    }
}

```
   
<br><br>

### @Table
> Entity 클래스와 DB 테이블 간의 매핑을 정의할 때 사용
- 매개변수
    - name : 테이블의 이름 지정
    - schema : 스키마의 이름 지정
    - uniqueConstraints : 고유 제약 조건 지정   
```java
@Table(name="USER_TB", scehma="test", uniqueConstraints ={@UniqueConstraint(columnNames = {"email"})}) 
@Entity
public class User {
    // ...
}
```
<br>

### @Entity
> 클래스가 JPA entity 임을 나타냄
- DB table 과 1:1 매핑되며 JPA가 관리하는 영속성 유닛의 일부가 된다.
```java
@Entity
public class User {
    // ...
}
```
<br>

### @Id
> 해당 필드를 기본키(PK)로 설정
```java
@Table(name="users")
@Entity
public class User implements UserDetails {
    @Id
    private Long id;
}
```
<br>

### @GeneratedValue
> 기본 키의 값을 생성하는 전략을 지정할 때 사용한다.
- 매개변수
    - strategy : 기본 키 생성 전략을 지정한다.
        - GenerationType 열거 형의 값 중 하나를 사용할 수 있다.
            - AUTO
            - IDENTITY
            - SEQUENCE
            - TABLE
    - generator : 기본 값 이외의 사용자 정의 생성기를 지정할 때 사용한다.
```java
@Entity
public class User implements UserDetails {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
```
<br>

### @Column
> Entity 클래스와 DB 테이블 간의 매핑을 정의할 때 사용
- 매개변수
    - name : 데이터베이스 컬럼명 명시 (default : 필드의 이름과 동일)
    - nullable :널 값 허용 여부 (default : true)
    - unique : 고유 제약 조건을 부여할지 여부 (default : false)
    - length : 문자열 컬럼의 길이를 지정 (default : 255)

```java
@Entity
public class User implements UserDetails {
    @Id
    @Column(name = "id", updatable = false)
    private Long id;
}
```
   
<br><br>