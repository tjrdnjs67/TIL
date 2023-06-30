- **@SpringBootTest** : 스프링 컨테이너와 테스트를 함께 실행한다.
- **@Transactional** : 테스트 케이스에 이 에노테이션이 있으면, 테스트 시작 전에 트랜잭션을 시작하고, 테스트 완료 후에 항상 롤백한다. 이렇게 하면 DB에 데이터가 남지 않으므로 다음 테스트에 영향을 주지 않는다.

### AOP 적용 전

![Alt text](/img/spring_img/aop1.png)

### AOP 적용 후

![Alt text](/img/spring_img/aop2.png)

1. 스프링 컨테이너는 AOP가 있으면 프록시 memberService를 만들어서 빈으로 등록한다.
2. 프록시 memberService에서 **joinPoint.proceed()** 가 실행되면 그때 진짜 memberService가 실행된다.


![Alt text](/img/spring_img/aop3.png)