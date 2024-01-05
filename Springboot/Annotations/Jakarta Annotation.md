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