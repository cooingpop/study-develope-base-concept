# study-develope-base-concept

### 스프링부트

Spring Boot는 개발의 simpify를 최우선으로 한 java framework입니다.
Spring Boot는 Spring MVC 기반의 Java Web 개발을 더 쉽게 만들어주는 특징은 다음과 같습니다.

- auto-configuration
- embedded servlet container
- starter-dependencies
- Actuator
- Spring Boot CLI

### Spring Boot와 Spring MVC의 차이점

둘 다, 스프링 프레임워크의 범주에 포함됩니다. 각각 다른 문제를 해결하기 위한 프레임워크입니다. 

Spring MVC는 Model-View-Controller 디자인패턴을 사용하는 일관된 구조를 제공함으로써 자바 웹 개발을 쉽게 하게 해줍니다. 반면, 스프링부트는 Spring MVC를 포함하는 Spring framework를 가지고 웹 개발을 하면서 가지는 고통스러운 설정, 의존성 관리 그리고 애플리케이션 실행을 더 간편하고 쉽게 개발하게 해줍니다.

### Spring Boot 장점

- starter를 통한 자동 권장 버전 관리, 편리한 의존성 관리
- 내장서버가 있기때문에 jar 파일로 간단하게 배포 가능

IOC - 객체의 생성 생명주기의 관리까지 모든 객체에 대한 제어권이 바뀌었다는 것을 말합니다.
   객체를 생성 및 제거하는 것은 비용이 많이 들기 때문에 스프링 컨테이너에서 IOC를 구현해주어 자주 사용하는 객체를 제어함
DI - 의존성 주입으로 의존적인 객체를 직접 생성하거나 제어하는것이 아니라 외부에서 결정해서 연결시키는것
   @Componet 어노테이션으로 의존객체로 만들고 



AOP - 공통기능을 모든 모듈에 적용하기 위한 방법
\- 관점지향프로그래밍 메소드 전 후 지점에 설정 가능하며 트랜잭션, 에러처리와 같은 기능에 적합함
    (로깅', '트랜잭션', '에러 처리')
   @Transactional, interceptor, filter aop의 일종
@Before: 대상 메서드의 수행 전
@After: 대상 메서드의 수행 후
@After-returning: 대상 메서드의 정상적인 수행 후
@After-throwing: 예외발생 후
@Around: 대상 메서드의 수행 전/후

Filter - 서블릿 필터는 DispatcherServlet 이전에 실행이 되는데 필터가 동작하도록 지정된 자원의 앞단에서 요청내용을 변경하거나, 여러가지 체크를 수행할 수 있다.

 init() - 필터 인스턴스 초기화
ㆍdoFilter() - 전/후 처리
ㆍdestroy() - 필터 인스턴스 종료

Interceptor - 컨트롤러를 호출하기 전 후단계에 대한 요청 응답에 대해 처리함 
       (로그인체크, 권한체크)
preHandler() - 컨트롤러 메서드가 실행되기 전
postHanler() - 컨트롤러 메서드 실행직 후 view페이지 렌더링 되기 전
afterCompletion() - view페이지가 렌더링 되고 난 후

### 디자인패턴

- 싱글턴패턴 - 객체를 하나만 생성해서 생성된 객체를 어디에서든지 참조할수 있도록 하는 패턴 
       (고정된 메모리 영역을 얻으면서 한번의 new로 인스턴스를 사용하기 떄문에 메모리 낭비를 방지할수있음) 
      private로 외부에서 접근못하도록하고 instance 함수를 만들어 그 안에 new로 객체생성
- 전략패턴 - 객체가 할 수 있는 행위들 각각을 전략으로 만들어 놓고 수정이 필요한 경우 전략을 바꾸는 것만으로 행위의 수정이 가능하도록 만든 패턴입니다.
- 템플릿 메서드 패턴 - 서브 클래스로 캡슐화해 구조는 바꾸지 않고 상황에 맞게 서브클래스를 이용해 수행 내역을 변경해주는 패턴
- 커멘트패턴 - 실행될 기능을 캡슐화 함으로써 주어진 여러 기능을 실행할 수 있는 재사용성이 높은 클래스 설계하는 패턴
- 빌더패턴 - 여러개의 파라미터를 전달할때도 어떤한값이 어떤한 의미인지 파악할수 있어서 사용, 유지보수에 용이함
  어댑터와 프록시 패턴(두 클랙스간에 하나의 클래스를 두는 구조)
  차이점- 어댑터는 하나의 인터페이스에 맞추는게 목적이고 
     프록시는 다양한 방식으로 로직 컨트롤이 목적

타임리프 장점
\- 템플릿 코드 자체가 html이기 때문에 뷰파일을 was없이도 브라우저에서 직접 띄워볼수가있음

## Spring Boot @SpringBootApplication 내부

@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(
excludeFilters = {@Filter(
type = FilterType.CUSTOM,
classes = {TypeExcludeFilter.class}
), @Filter(
type = FilterType.CUSTOM,
classes = {AutoConfigurationExcludeFilter.class}
)}
)

대표적으로 @SpringBootConfiguration, @EnableAutoConfiguration ,@ComponentScan 3가지가있다.

- @SpringBootConfiguration: 스프링 부트의 설정을 나타내는 어노테이션이다. 스프링의 @Configuration을 대체하며 스프링 부트 전용 어노테이션이다. 테스트 어노테이션을 사용할 때 계속 이 어노테이션을 찾기 때문에 스프링 부트에서는 필수 어노테이션이다.
- @EnableAutoConfiguration: 자동 설정의 핵심 어노테이션이다. 클래스 경로에 지정된 내용을 기반으로 설정 자동화를 수행한다.
- @ComponentScan: basePackages 프로퍼티 값에 별도의 경로를 설정하지 않으면 해당 어노테이션이 위치한 패키지가 루트 경로가 된다.

클래스
\- 클래스는 유사한 특징을 지닌 객체들의 속성을 묶어놓은것

인스턴스
\- 기능들의 집합이고 연관된 클래스에서 작성됨.

GC
\- heap영역의 오브젝트 중 stack에서 도달 불가능한 오브젝트들은 가비지 컬렉션의 대상이됨

### auto-configuration

Spring Boot auto-configuration가 classpath를 체크합니다. 체크해서 예를 들어 thymeleaf가 있으면, Thymelead template resolver, view resolver, and a template engine 이 것들을 자동으로 설정해 줍니다.

만약, Spring Data JPA가 classpath에 있으면, 자동으로 repository interface들로부터 repository implementations를 만들어줍니다.

## Spring Annotation

- @Component
  component-scan을 선언에 의해 특정 패키지 안의 클래스들을 스캔하고, @Component Annotation이 있는 클래스에 대하여 bean 인스턴스를 생성한다.
  @Controller, @Service, @Repository
  @Component —구체화—> @Controller, @Service, @Repository
  bean으로 등록
  해당 클래스가 Controller/Service/Repository로 사용됨을 Spring Framework에 알린다.

- @RestController
  @Controller + @ResponseBody
  @ResponseBody를 모든 메소드에서 적용한다.
  메소드의 반환 결과(문자열)를 JSON 형태로 반환한다.

  

- @Controller 와 @RestController 의 차이
  @Controller
  API와 view를 동시에 사용하는 경우에 사용
  대신 API 서비스로 사용하는 경우는 @ResponseBody를 사용하여 객체를 반환한다.
  view(화면) return이 주목적
  @RestController
  view가 필요없는 API만 지원하는 서비스에서 사용 (Spring 4.0.1부터 제공)

  

- @RequestMapping 메서드가 기본적으로 @ResponseBody 의미를 가정한다.
  data(json, xml 등) return이 주목적
  즉, @RestController = @Controller + @ResponseBody

## Bean 생명주기



## Spring Boot Starter Dependency

### Starter dependency란?

starter dependency는 스프링부트에서 의존성 관리 문제를 해결해주는 역할을 합니다. 우리가 스프링부트를 사용할 때, JPA나 Thymeleaf Template가 현재 프로젝트에 적합한 버전이 무엇인지 알아야하거나 필요한 의존성 리스트를 상세하게 알 필요가 없습니다. 단지 Gradle이나 Maven build file에 추가해주면됩니다.

starter가 Maven이나 Gradle file에 등록한 의존성jar를 자동으로 프로젝트에 로드해 줍니다.
spring-boot-starter-web를 의존성 추가하면, Spring MVC Jar를 프로젝트에 import합니다.

 

###### 구동원리

- spring-boot-maven-plugin : mvn package 실행 시 해당 메이븐 프로젝트를 하나의 .jar 파일로 묶어주는 역할

- org.springframework.boot.loader.jar.JarFile : 내장 .jar 파일들, 외부 라이브러리 파일들을 읽음
- org.springframework.boot.loader.launcher : .jar 파일 실행



### 스프링부트에서 properties정의

 application.properties파일에 정의하면 되고, springboot가 자동으로 읽습니다. 예로 server.port=9000으로 하면, 내장 톰켓이 실행되면, 디폴트 8080이 아니라 9000으로 앱이 실행됩니다.

 

### YML

YAML(야믈, 와이엠엘(.yml))은 JSON의 상위집합(superset)으로, 계층적 뼈대 구조를 설정하는데 편리한 형식(format)입니다. SpringApplication은 classpath에 있는 [SnakeYAML](https://bitbucket.org/asomov/snakeyaml) library를 가지고 있을 때, 속성(properties)의 대안으로 자동적으로 YAML을 지원합니다.

> spring-boot-starter는 가장 기본적인 라이브러리고, 이것이 있으면 SnakeYAML 은 자동으로 제공됩니다.

 

### JAVA8 Stream

JDK 8에서 추가된 Stream API

컬렉션, 배열등의 저장 요소를 하나씩 참조하며 함수형 인터페이스(람다식)를 적용하며 반복적으로 처리할 수 있도록 해주는 기능

 

### POJO(Plain Old Java Object) 

POJO는 말 그대로 해석을 하면 오래된 방식의 간단한 자바 오브젝트 
쉽게 생각해서 순수한 자바 오브젝트라고 생각하면된다 
예) getter, setter 가 메소드로 이루어진 Value Object 라고 생각하면된다.

 

### **비동기 (Asynchronous: 동시에 일어나지 않는, 非同期: 같은 시기가 아닌)**

비동기란 말 그대로 동시에 일어나지 않는다는 의미한다.
즉, 요청과 결과가 동시에 일어나지 않아 바로 결과가 주어지지 않고 나중에 처리된다

### **동기 (synchronous: 동시에 일어나는, 同期: 같은 시기)**

동기란 비동기와 반대로 동시에 일어난다는 말한다. 따라서 요청과 그 결과가 동시에 일어나서 
요청을 하면 바로 그 요청한 자리에서 결과가 주어지며
시간이 얼마가 걸리든 상관 안하고 요청한 그 자리에서 결과를 주겠다는 약속같은 것이다.
즉, 요청과 결과가 한자리에서 동시에 일어난다

\* 이렇게 동기와 비동기를 구분하는 이유는
동기와 비동기를 굳이 구분하는 이유는 상황에 따라서 장단점이 있기 때문인데
동기방식은 매우 설계가 간단하고 직관적이지만, 결과가 주어질 때까지 아무것도 못하고 대기해야 하는 단점이있고
비동기방식은 좀더 복잡하지만 결과가 주어지는 시간이 길어져도 그 시간 동안 다른 작업을 할 수 있으므로 좀더 효율적으로 자원을 사용할 수 있는 장점이있다

### **블로킹(Blocking)**

블로킹은 말 그대로 작업이 중단된다는 의미. 네트워크 통신에서 요청이 발생하고 완료될 때까지 모든 일을 중단한 상태로 대기해야 하는 것을 블로킹 방식이라 한다.

### **논블로킹(Non-blocking)**

논블러킹은 말 그대로 중단되지 않는다는 말. 통신이 완료 될 때까지 중단되는 블로킹의 반대 개념이다.
논블로킹 방식은 아무래도 통신이 완료될 때까지 기다리지 않고 다른 작업을 수행할 수 있으므로 경우에 따라 효율이나 반응속도가 더 뛰어나다.



## Rest

- Representational State Transfer의 약자
- 자원을 표현(이름)으로 구분하여 해당 자원의 정보를 주고 받는 모든 것을 의미한다.
- 자원은 해당 소프트웨어가 관리하는 모든 것(문서, 그림, 데이터, 해당 소프트 웨어 자체 등)
- 자원의 표현은 그 자원을 표현하기 위한 이름이다.
- 정보를 전달하는 것은 데이터가 요청되어지는 시점에서 자원의 상태(정보)를 전달한다.
- 즉 json혹은 xml를 통해 데이터를 주고 받는 것으로 생각하자

 

## REST API

- API는 데이터와 기능의 집합을 제공하여 컴퓨터 프로그램간 정보 교환이 가능하도록 하는 것
- REST API는 REST를 기반으로 서비스 API를 구현한 것
- 사내 시스템들도 REST 기반으로 시스템을 분산해 확장성과 재사용성을 높여 유지보수 및 운용을 편리하게 할 수 있다.
- REST는 HTTP 표준을 기반으로 구현하고, HTTP를 지원하는 프로그램 언어로 클라이언트, 서버를 구현할 수 있다.

 

## 비동기 처리

1) 비동기는 무슨 동기로 존재하는가?

- 자바스크립트의 비동기 처리란 특정 코드의 연산이 끝날 때까지 코드의 실행을 멈추지 않고 다음 코드를 먼저 실행하는 자바스크립트의 특성을 의미한다. 내가 이해한 바로는 상당히 성격이 급한 녀석이다. 어떤 코드를 보고 컴퓨터에게 연산을 요청한 후 바로 다음 코드로 넘어가버리는 것이다. 로직의 실행이 끝날 때까지 기다려주지 않고 다음 코드를 먼저 실행하는 것이 비동기 처리이다.
- 자바스크립트는 브라우저 위에서 사용하는 언어이다. 자바스크립트는 기본적으로 통신이라는 개념을 가지고 있고 통신 중 어떤 함수가 일 처리가 길어지면, 웹 브라우저는 계속 멈춤 상태가 되고 기다려야 된다. 이 상황을 방지하기 위해 비동기 방식을 가지게 된다.

2) 그럼 어떤 사례가 있는가?

- ajax
  비동기 처리의 가장 흔한 사례는 제이쿼리의 ajax이다. 제이쿼리로 실제 웹 서비스를 개발할 때 ajax 통신을 뺴놓을 수가 없다. 보통 화면에 표시할 이미지나 데이터를 서버에서 불러와 표시해야 하는데 이때 ajax통신으로 해당 데이터를 서버로부터 가져올 수 있기 때문이다.
- setTimeOut()
  Web API의 한 종류, 코드를 바로 실행하지 않고 지정한 시간만큼 기다렸다가 로직을 실행한다.

## 콜백 함수

1) 기본 정의

- 콜백함수는 함수 안에서 어떤 특정한 시점에 호출되는 함수를 말한다.
- 보통 콜백 함수는 함수의 매개변수로 전달하여 특정 시점에서 콜백 함수를 호출한다.

2) 콜백 함수를 사용하는 이유!!!!!!!!

- 웹사이트의 동작에 해당하는 코드일 경우 로직이 복잡해서 처리속도가 늦어지게 된다면 실행이 지연되고 웹사이트가 로직이 해결되기 전까지 모든 동작을 멈춰버린다.
- 반면 콜백 함수를 사용하면 필요한 연산이 완료될 때 까지 뒤에 있는 가벼운 로직들을 처리할 수 있다. 즉 정말로 필요할 때만 함수를 호출해서 효율이 좋고 웹사이트에서도 여러 가지 동작을 동시에 할 수 있다.

3) 마지막으로 다시 정리

- 콜백 함수의 동작 방식은 식당 자리 예약에 비유할 수 있다. 항상 줄이 긴 맛집에 가기 위해 똑똑한 우리는 문명의 발전을 사용하여 미리 주문을 하는 기막힌 방법을 찾아낸다. 미리 시켜두고 사무실에서 뒹굴다가, 책보다가, 일하다가, 눕다가, 일어났다가, 커피마시다가 시간되면 가면된다.

4) 대표적인 예

- oauth 토근 생성시 callback url을 전달해줘야 하며 그 url에 결과를 전달해줌.

 

### WebFlux

 적은 양의 스레드와 최소한의 하드웨어 자원으로 동시성을 핸들링하기 위해 만들어졌다. 서블릿 3.1이 논블로킹을 지원하지만, 일부분이다. 이는 새로운 공통 API가 생긴 이유가 됐으며, netty와 같은 잘 만들어진 async, non-blocking 서버를 사용한다.

비동기 논블로킹 환경에서 자리를 잡은 서버(e.g. Netty) spring 버전이라고 생각하면된다.

- 비동기 - 논블록킹 리액티브 개발에 사용
- 효율적으로 동작하는 고성능 웹어플리케이션 개발
- 서비스간 호출이 많은 마이크로서비스 아키텍처에 적합





