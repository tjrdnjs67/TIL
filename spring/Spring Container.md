스프링 컨테이너 생성 스프링 컨테이너가 생성되는 과정을 알아보자. 

```
//스프링 컨테이너 생성 
ApplicationContext applicationContext = 
new AnnotationConfigApplicationContext(AppConfig.class);
```

- ApplicationContext 를 스프링 컨테이너라 한다. 
- ApplicationContext 는 인터페이스이다. 
- 스프링 컨테이너는 XML을 기반으로 만들 수 있고, 애노테이션 기반의 자바 설정 클래스로 만들 수 있다. 
- 직전에 AppConfig 를 사용했던 방식이 애노테이션 기반의 자바 설정 클래스로 스프링 컨테이너를 만든 것이다. 
- 자바 설정 클래스를 기반으로 스프링 컨테이너( ApplicationContext )를 만들어보자. 
	- new AnnotationConfigApplicationContext(AppConfig.class); 
	- 이 클래스는 ApplicationContext 인터페이스의 구현체이다. 


	참고: 더 정확히는 스프링 컨테이너를 부를 때 BeanFactory , ApplicationContext 로 구분해서 이야기 한다. 이 부분은 뒤에서 설명하겠다. BeanFactory 를 직접 사용하는 경우는 거의 없으므로 일반적으로 ApplicationContext 를 스프링 컨테이너라 한다.


![Alt text](/img/spring_img/spring-container.png)

- new AnnotationConfigApplicationContext(AppConfig.class)
- 스프링 컨테이너를 생성할 때는 구성 정보를 지정해주어야 한다.
- 여기서는 AppConfig.class 를 구성 정보로 지정했다


![Alt text](/img/spring_img/spring-container2.png)

- 스프링 컨테이너는 파라미터로 넘어온 설정 클래스 정보를 사용해서 스프링 빈을 등록한다. 
- 빈 이름 빈 이름은 메서드 이름을 사용한다. 
- 빈 이름을 직접 부여할 수 도 있다. 
	- @Bean(name="memberService2")


![Alt text](/img/spring_img/spring-container3.png)



![Alt text](/img/spring_img/spring-container4.png)
- 스프링 컨테이너는 설정 정보를 참고해서 의존관계를 주입(DI)한다.
- 단순히 자바 코드를 호출하는 것 같지만, 차이가 있다. 이 차이는 뒤에 싱글톤 컨테이너에서 설명한다.


**참고**
스프링은 빈을 생성하고, 의존관계를 주입하는 단계가 나누어져 있다. 그런데 이렇게 자바 코드로 스프링 빈을 등록하면 생성자를 호출하면서 의존관계 주입도 한번에 처리된다. 여기서는 이해를 돕기 위해 개념적으로 나누어 설명했다. 자세 한 내용은 의존관계 자동 주입에서 다시 설명하겠다. 

**정리** 
스프링 컨테이너를 생성하고, 설정(구성) 정보를 참고해서 스프링 빈도 등록하고, 의존관계도 설정했다. 
이제 스프링 컨테이너에서 데이터를 조회해보자