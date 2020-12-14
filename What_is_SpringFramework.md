# Spring Framework란 무엇인가
## Spring Framework란?
자바 플랫폼을 위한 오픈소스 어플리케이션 프레임워크로서 엔터프라이즈급 어플리케이션을 개발하기 위한 모든 기능을 종합적으로 제공하는 경량화된 솔루션이다.  
엔터프라이즈급 개발이란 기업을 대상으로 하는 개발이란 뜻이다.  
즉, 대규모의 데이터 처리와 트랜잭션이 동시에 여러 사용자로부터 행해지는 매우 큰 규모의 환경을 엔터프라이즈 환경이라 한다.

## 컨테이너란
프레임워크 안에서 인스턴스들의 생명 주기를 관리하며, 생성된 인스턴스들에게 추가적인 기능을 부여하는 역할을 한다.  
자기가 작성한 코드의 처리과정을 컨테이너에서 수행한다.  
스프링 컨테이너는 스프링 프레임워크 핵심에 위치하며, DI를 통해 애플리케이션을 구성하는 컴포넌트들을 관리한다.  
Lifecycle Mangement, configuration, Dependency Resolution, Object pooling 등을 관리한다.

## IOC란
IOC는 Inversion of Control의 약자로 말 그대로 제어의 역전이라 한다.  
일반적으로 지금까지의 프로그램은 객체 결정 및 생성 -> 의존성 객체 생성 -> 객체 내의 메서드 호출하는 작업을 반복하였습니다.  
이는 각 객체들이 프로그램의 흐름을 결정하고 각 객체를 구성하는 작업을 직접적으로 참여한 것이다.  
**즉, 모든 작업을 사용자가 제어하는 구조인 것이다.**  

하지만 IOC에서는 이 흐름의 구조를 바꾼다.  
IOC에서의 객체는 자기가 사용할 객체를 선택하거나 생성하지 않고, 자신이 어디서 만들어지고 어떻게 사용되는지 모른다.  
자신의 모든 권한을 다른 대상에 위임함으로써 제어권한을 위임받은 특별한 객체에 의해 결정되고 만들어진다.  
**즉, 제어의 흐름을 사용자가 컨트롤 하지 않고 위임한 특별한 객체에 모든 것을 맡기는 것**이다.

**IOC란 기존 사용자가 모든 작업 권한을 제어하던 것을 특별한 객체에 모든 것을 위임하여 객체의 생성부터 생명주기 등 모든 객체에 대한 제어권이 넘어간 것을 IOC, 제어의 역전**이라고 한다.

## IOC의 구성요소
IOC는 DI와 DL의 의해 구현된다.  

DL(Dependency Lookup) - 의존성 검색  
컨테이너는 객체들을 관리하기 위해 별도의 저장소에 빈을 저장하는데, 저장소에 저장되어 있는 빈을 개발자들이 컨테이너에서 제공하는 API를 이용하여 사용하고자 하는 빈을 검색하는 방법이다.

DI(Dependency Injection) - 의존성 주입
의존성 주입이란 객체가 서로 의존하는 관계가 되게 의존성을 주입하는 것이다. 객체지향 프로그램에서 의존성이란 하나의 객체가 어떠한 다른 객체를 사용하고 있음을 의미한다.  
IOC에서 DI는 **각 클래스 사이에 필요로 하는 의존관계를 빈 설정 정보를 바탕으로 컨테이너가 자동 연결**해주는 것이다.  
의존적인 객체를 직접 생성하거나 제어하는 것이 아니라, 특정 객체에 필요한 객체를 외부에서 결정해서 연결해주는 것이다.
![screensh](https://media.vlpt.us/images/dnjscksdn98/post/9be17568-4801-44fb-af85-7f81f6ef6c55/spring_mvc_flow.png)


## Spring Framework의 흐름
1. 요청된 URL을 dispartcher-servlet으로 전달
2. 핸들러 매핑은 해당 URL에 매핑된 컨트롤러가 있는지 검사 후 컨트롤러에 전달
3. 해당 컨트롤러의 로직 수행
4. ModelAndView 객체 생성 후, 로직의 결과를 담아서 dispartcher-servlet에 전달
5. dispartcher-servlet은 전달받은 뷰가 있는지 검사하기 위해 ViewResolver로 전송
6. ViewResolver는 받은 뷰가 있는지 검사 후 뷰로 전송
7. 모델과 같이 뷰를그린 후 dispartcher-servlet으로 전송
8. 최종적으로 컨텐츠를 클라이언트에게 전송

## Spring Framework의 특징 POJO
POJO(Plan Old Java Object)는 말 그대로 평범한 자바 오브젝트이다.  
이전 EJB(Enterprise JavaBeans)는 확장 가능한, 재사용이 가능한 로직을 개발하기 위해 사용되었다.  
EJB는 한가지 기능을 위해 불필요하고 복잡한 로직이 과도하게 들어가있다는 단점이 있다.  
그래서 다시 조명을 받은게 바로 POJO이다.
POJO는 Getter/Setter를 가진 단순 자바 오브젝트로 정의를 하고 있다.  
이러한 단순 오브젝트는 의존성이 없고 추후 테스트 및 유지보수가 편리하고 유연성의 장점을 가진다.  
이러한 장점들로 인하여 객체지향적인 다양한 설계와 구현이 가능해지고, POJO의 기반의 Framework가 조명을 받고 있다.

**POJO를 사용함으로써 코드는 더욱 심플해졌고 테스트 하기에 더 좋아졌으며, 유연하고 요구사항에 따라 기술적 선택을 바꿀 수 있도록 바뀌었다.**

## Spring Framework의 특징 AOP
AOP(Aspect Oriented Programming)란 말 그대로 관점 지향 프로그래밍이다.  
대부분 소프트웨어 개발 프로세스에서 사용하는 방법은 OOP(Object Oriented Programming)이다.  
OOP는 객체지향 원리에 따라 관심사가 같은 데이터를 한 곳에 모아 분리하고, 낮은 결함도를 갖게하여 독립적이고 유연한 모듈로 캡슐화하는 것을 일컫는다.  
이러한 과정 중 중복된 코드들이 많아지고 가독성과 확장성, 유지보수성을 떨어뜨린다.  
이러한 문제를 보완하기 위해 나온 것이 AOP이다.  

AOP에서는 핵심기능과 공통 기능을 분리시켜 핵심 로직에 영향을 끼치지 않게 공통 기능을 끼워 넣는 개발 형태이며, 이렇게 개발함에 따라 **무분별하게 중복되는 코드를 한 곳에 모아 중복되는 코드를 제거하여, 공통 기능 한 곳에 보관함으로써 공통 기능 하나의 수정으로 모든 핵심 기능들의 공통 기능을 수정할 수 있어 효율적인 유지보수가 가능하며 재사용성을 극대화**해준다.  
물론 AOP로 만들 수 있는 기능은 OOP로 구현할 수 있지만, Spring에서는 AOP를 편리하게 사용할 수 있도록 지원하고 있다.

## Spring Framework의 특징 MVC(Model2)
![screensh](https://t1.daumcdn.net/cfile/tistory/9929B2345B9E4E002D)  
MVC(Model View Controller)란 구조로 사용자 인터페이스와 비지니스 로직을 분리하여 개발하는 것이다.  
MVC에서는 Model1과 Model2로 나누어져 있으며, 일반적으로 MVC는 Model2를 지칭한다.

### **Model**
Model에서는 데이터처리를 담당하는 부분이다.  
Service 영역과 DAO영역으로 나누어지게 되고, Service 부분은 불필요하게 HTTP통신을 하지 않아야 하며 Request나 Response와 같은 객체를 매개변수로 받아서는 안된다.  
또한 Model부분의 Service는 view에 종속적인 코드가 없어야 하고, View부분이 변경된다 하더라도 Service부분은 그대로 재사용할 수 있어야 한다.  
**Model에서는 View와 Controller에 대한 어떤 정보도 가지고 있어서는 안된다.**

### **View**
View는 사용자 Interface를 담당하며, 사용자에게 부여지는 부분이다.  
View는 Controller를 통해 모델에 데이터에 대한 시각화를 담당하며, View는 자신이 요청을 보낼 때 Controller의 정보만 알고 있어야 한다.  
**Model이 가지고 있는 정보를 저장해서는 안되며 Model, Controller의 구성 요소를 알아서는 안된다.**

### **Controller**
Controller에서는 View에서 받은 요청을 가공하여 Model(Service 영역)에 이를 전달한다.  
또한 Model로부터 받은 결과를 View로 넘겨주는 역할을 한다.  
Controller에서는 모든 요청 에러가 모델 에러를 처리하며 View와 Model의 정보를 알아야 한다.  
**Model과 View의 정보에 대해 알고있어야 한다.**

Model, View, Controller를 분리하여 각 소스의 목적을 명확하게 하고, 유지보수 하는데에 용이하게 한다.  
**모둘화를 통해 어디서든 재사용이 가능하다.**

## Spring Framework의 구조
![screensh](https://t1.daumcdn.net/cfile/tistory/99A523405B9E2C1510)

## Spring Core
- Spring Container를 의미함
- core라는 말 그대로 Spring Framework의 핵심이며, 그중 핵심은 Bean Factory Container
- Bean Factory는 IOC패턴을 적용하여 객체 구성 부터 의존성 처리까지 모든 일을 처리하는 역할을 함

## Spring Context
- Spring Framework의 context 정보들을 제공하는 설정 파일
- Spring Context에는 JNDI, EJB, Validation, Scheduiling, Internaliztaion 등 엔터프라이즈 서비스들을 포함

## Spring AOP
- Spring Framework에서 관점지향 프로그래밍을 할 수 있고 AOP를 적용 할수 있게 도와주는 Module

## Spring DAO
- Data Access Object의 약자로 Database Data에 접근하는 객체
- Spring JDBC DAO는 추상 레이어를 지원함으로써 코딩이나 예외처리 하는 부분을 간편화 시켜 일관된 방법으로 코드를 짤 수 있게 도와줌

## Spring ORM
- Object relational mapping의 약자로 간단하게 객체와의 관계 설정을 하는 것
- Spring에서는 Ibatis, Hibernate, JDO 등 인기있는 객체 관계형 도구(OR도구)를 사용 할 수 있도록 지원

## Spring Web
- Web context module은 Application module에 내장 및 Web기반의 응용프로그램에 대한 Context를 제공하여 일반적인 Web Application 개발에 필요한 기본적인 기능을 지원
- Jakarta Structs 와의 통합을 지원

## Spring MVC
- Model2 구조로 Apllication을 만들 수 있도록 지원
- 웹 응용 프로그램을 작성하기위한 완전한 기능을 갖춘 MVC를 구현
- 전략 인터페이스를 통해 고급 구성 가능하며 JSP, Velocity, Tiles, iText 및 POI를 포함한 수많은 뷰 기술을 지원