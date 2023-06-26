
### 1. 정적 컨텐츠
	- 단순히 Server에서 파일을 웹브라우저로 내려주는 방식
	- src/resources/static 에서 정적 파일을 생성하면 ex) hello-static.html http://localhost:8080/hello-static.html 웹브라우저에 치면 해당 파일을 내려 받을 수 있다.

![Alt text](/img/spring_img/static-image.png)
1. 내장 톰켓 서버가 http://localhost:8080/hello-static.html에 대한 요청을 받는다.
2. 먼저 스프링 컨테이너에서 hello-static 관련 controller가 있는지 찾아본다.
3. 만약 2번에서 없었다면 resources/static 에서 hello-static.html을 찾는다.

### MVC와 템플릿 엔진
	- JSP, PHP 등이 템플릿 엔진
	- Model, View, Controller
	- 서버에서 프로그래밍을 해서 html을 동적으로 바꾼 후 웹브라우저로 내려주는 방식

**Model 1 방식** : Controller, View(JSP)로 나누지 않고 View(JSP)에서 모든 일을 처리하는 방식

Model 2 방식 : View(JSP)에서 출력만 처리

![Alt text](/img/spring_img/template-engine.png)
1. 내장 톰켓 서버가 http://localhost:8080/hello-mvc 대한 요청을 받는다.
2. 스프링 컨테이너에서 hello-mvc 관련 controller가 있는지 찾아본다.
3. viewResolver에서 view를 찾아서 템플릿 엔진과 연결해준다.
4. 템플릿 엔진이 렌더링을 해서 변환된 html을 웹브라우저에 반환한다.


### API
	- json이라는 데이터 포멧으로 클라이언트한테 데이터를 전달해주는 방식

![Alt text](/img/spring_img/api.png)
1. 내장 톰켓 서버가 http://localhost:8080/hello-api 대한 요청을 받는다.
2. @ResponseBody가 어노테이션으로 붙어 있으면 HTTP의 BODY에 문자 내용을 직접 반환
3. viewResolver 대신에 HttpMessageConverter가 동작
4. 기본 문자처리 : StringHttpMessageConverter
5. 기본 객체처리 : MappingJackson2HttpMessageConverter
6. byte 처리 등등 기타 여러 HttpMessageConverter가 기본으로 등록되어 있음