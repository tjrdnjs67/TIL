
![Alt text](/img/spring_img/bean-factory.png)

**BeanFactory**
- 스프링 컨테이너의 최상위 인터페이스
- 스프링 빈을 관리하고 조회하는 역할을 담당
- getBean()을 제공
- 지금까지 사용했던 기능은 BeanFactory가 제공하는 기능


**ApplicationContext**
- BeanFactory 기능을 모두 상속받아서 제공
- 빈을 관리하고 검색하는 기능을 BeanFactory가 제공해주는데, 차이점이 뭘까?
- 애플리케이션을 개발할 때는 빈을 관리하고 조회하는 기능은 물론이고, 수많은 부가기능이 필요

![Alt text](/img/spring_img/bean-factory2.png)
- **메시지소스를 활용한 국제화 기능**
	-  예를 들어서 한국에서 들어오면 한국어로, 영어권에서 들어오면 영어로 출력
- **환경변수**
	-  로컬, 개발, 운영등을 구분해서 처리
- **애플리케이션 이벤트**
	-  이벤트를 발행하고 구독하는 모델을 편리하게 지원
- **편리한 리소스 조회**
	-  파일, 클래스패스, 외부 등에서 리소스를 관리하게 조회

**정리** 
- ApplicationContext는 BeanFactory의 기능을 상속받는다.
- ApplicationContext는 빈 관리기능 + 편리한 부가 기능을 제공한다. 
- BeanFactory를 직접 사용할 일은 거의 없다. 부가기능이 포함된 ApplicationContext를 사용한다.
- BeanFactory나 ApplicationContext를 스프링 컨테이너라 한다.


### 스프링 빈 설정 메타 정보 - BeanDefinition 

- 스프링은 어떻게 이런 다양한 설정 형식을 지원하는 것일까? 그 중심에는 BeanDefinition 이라는 추상화가 있다. 
- 쉽게 이야기해서 역할과 구현을 개념적으로 나눈 것이다!
	- XML을 읽어서 BeanDefinition을 만들면 된다. 
	- 자바 코드를 읽어서 BeanDefinition을 만들면 된다. 
	- 스프링 컨테이너는 자바 코드인지, XML인지 몰라도 된다. 오직 BeanDefinition만 알면 된다. 
- BeanDefinition 을 빈 설정 메타정보라 한다.
	- @Bean , 당 각각 하나씩 메타 정보가 생성된다.
- 스프링 컨테이너는 이 메타정보를 기반으로 스프링 빈을 생성한다.

![Alt text](/img/spring_img/bean-definition.png)


![Alt text](/img/spring_img/bean-definition2.png)
- AnnotationConfigApplicationContext 는 AnnotatedBeanDefinitionReader 를 사용해서 AppConfig.class 를 읽고 BeanDefinition 을 생성한다.
- GenericXmlApplicationContext 는 XmlBeanDefinitionReader 를 사용해서 appConfig.xml 설정 정보를 읽고 BeanDefinition 을 생성한다.
- 새로운 형식의 설정 정보가 추가되면, XxxBeanDefinitionReader를 만들어서 BeanDefinition 을 생성하면 된다.

**BeanDefinition 정보**
- BeanClassName: 생성할 빈의 클래스 명(자바 설정 처럼 팩토리 역할의 빈을 사용하면 없음)
- factoryBeanName: 팩토리 역할의 빈을 사용할 경우 이름, 예) appConfig
- factoryMethodName: 빈을 생성할 팩토리 메서드 지정, 예) memberService
- Scope: 싱글톤(기본값)
- lazyInit : 스프링 컨테이너를 생성할 때 빈을 생성하는 것이 아니라, 실제 빈을 사용할 때 까지 최대한 생성을 지연 처리 하는지 여부
- InitMethodName: 빈을 생성하고, 의존관계를 적용한 뒤에 호출되는 초기화 메서드 명
- DestroyMethodName: 빈의 생명주기가 끝나서 제거하기 직전에 호출되는 메서드 명
- Constructor arguments, Properties: 의존관계 주입에서 사용한다. (자바 설정 처럼 팩토리 역할의 빈을 사용 하면 없음