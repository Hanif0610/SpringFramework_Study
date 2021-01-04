# Servlet
## Servlet(서블릿)
서블릿을 한 줄로 정리하면 다음과 같다.
```
클라이언트의 요청을 처리하고, 그 결과를 반환하는 Servlet 클래스의 구현 규칙을 지킨 자바 웹 프로그래밍 기술
```
서블릿은 **자바를 사용하여 웹을 만들기 위해 필요한 기술**이다.  
클라이언트가 어떠한 요청을 하면 그에 대한 결과를 다시 전송해줘야 하는데, 이러한 역할을 하는 자바 프로그램이다.  
사용자가 로그인을 할 때 아이디와 비밀번호를 입력하고 로그인 버튼을 누르면, 서버에서는 아이디와 비밀번호를 확인 후 다음 페이지로 넘어간다.  
이러한 역할을 하는 것이 바로 Servlet(서블릿)이다.  
서블릿은 흔히 자바로 구현된 **CGI**라고 한다.

### **Servlet 특징**
- 클라이언트의 요청에 대하여 동적으로 작동하는 웹 어플리케이션 컴포넌트
- html을 사용하여 요청에 응답
- Java Thread를 이용하여 동작
- MVC 패턴에서 Controller에 이용된다.
- HTTP 프로토콜 서비스를 지원하는 javax.servlet.http.HttpServlet 클래스를 상속받는다.
- UDP보다 처리 속도가 느리다.
- HTML변경시 Servlet을 재컴파일 해야 한다.

일반적으로 웹 서버는 정적인 페이지만을 제공하기에, 동적인 페이지를 제공하기 위해서는 웹 서버가 다른곳에 도움을 요청하여 동적인 페이지를 작성해야 한다.  
동적인 페이지로는 임의의 이미지만을 보여주는 페이지와 같이 사용자가 요청한 시점에 페이지를 생성해서 전달해주는 것을 의미한다.  
여기서 웹서버가 동적인 페이지를 제공할 수 있도록 도와주는 어플리케이션이 서블릿이며, 동적인 페이지를 생성하는 어플리케이션이 CGI이다.

### **Servlet 동작 방식**
![screensh](https://t1.daumcdn.net/cfile/tistory/993A7F335A04179D20)  
1. 클라이언트가 URL을 입력하면 HTTP Request가 Servlet Container로 전송한다.
2. 요청을 전송받은 Servlet Container는 HttpServletRequest, HttpServletResponse 객체를 생성한다.
3. web.xml을 기반으로 하여 사용자가 요청한 URL이 어느 서블릿에 대한 요청인지 분석한다.
4. 해당 서블릿에서 Service메서드를 요청한 후 클라이언트의 GET, POST여부에 따라 doGet() 또는 doPost()를 호출한다.
5. doGet() or doPost() 메서드는 동적 페이지를 생성한 후 HttpServletResponse 객체에 응답을 보낸다.
6. 응답이 끝나면 HttpServletRequest와 HttpServletResponse 두 객체를 소멸시킨다.

```
CGI(Common Gateway Interface)  
CGI는 특별한 라이브러리나 도구를 의미하는것이 아닌, 별도로 제작된 웹 서버와 프로그램간의 교환방식이다.  
CGI방식은 어떠한 프로그래밍언어로도 구현이 가능하며, 별도로 만들어 놓은 프로그램에 HTML의 Get or Post 방법으로 클라이언트의 데이터를 환경변수로 전달하고, 프로그램의 표준 출력 결과를 클라이언트에게 전송하는 것이다.  
즉, 자바 어플리케이션 코딩을 하듯이 웹 브라우저용 출력 화면을 만드는 방법이다.
```

```
HTTP 프로토콜을 이용한 서버와의 통신 과정  
클라이언트는 정보를 얻기 위해 서버로 HTTP 요청을 전송하고, 서버는 이를 해석하여 정적 자원에 대한 요청일 경우 자원을 반환해주고, 그렇지 않은 경우 CGI 프로그램을 실행시켜 해당 결과를 리턴해준다.  
이때 서버는 CGI 프로그램에게 요청을 전달해주고, 결과를 전달받기 위한 파이프라인을 연결한다.  
그래서 CGI 프로그램은 입력에 대한 서비스를 수행하고, 결과를 클라이언트에게 전달하기 위해 결과 페이지에 해당하는 MINE 타입의 컨텐츠데이터를 웹 서버와 연결된 파이프라인에 출력하여 서버에 전달한다.  
서버는 파이프라인을 통해 CGI 프로그램에서 출력한 결과 페이지의 데이터를 읽어, HTTP응답 헤더를 생성하여 데이터를 함께 반환해준다.
```

## Servlet Container(서블릿 컨테이너)
서블릿 컨테이너는 말 그대로 서블릿을 관리해주는 컨테이너이다.  
서버에 서블릿을 만들었다고 해서 스스로 작동하는 것이 아니라 **서블릿을 관리해주는 것**이 필요한데 그러한 역할을 하는 것이 바로 서블릿 컨테이너 이다.  
서블릿이 어떠한 역할을 수행하는 정의서라고 한다면, 서블릿 컨테이너는 그 정의서를 보고 수행하는 역할을 한다고 볼 수 있다.  
서블릿 컨테이너는 **클라이언트의 요청을 받아주고 응답할 수 있도록 웹서버와 소켓으로 통신**한다.  
대표적인 예로 **톰켓(Tomcat)** 이 있다.  
톰켓은 실제로 웹 서버와 통신하여 JSP와 Servlet이 작동하는 환경을 제공해준다.

### **Servlet Container의 역할**
1. 웹 서버와의 통신 지원  
서블릿 컨테이너는 서블릿과 웹서버가 손쉽게 통신할 수 있도록 해준다.  
일반적으로 소켓을 만들고 listen, accept 등을 해야하지만 서블릿 컨테이너는 이러한 기능을 API로 제공하여 복잡한 과정을 생략할 수 있게 해준다.  
이러한 이점을 통해 개발자가 서블릿에 구현해야 할 비지니스 로직에 대해서만 초점을 두게끔 해준다.

2. 생명주기(Life Cycle) 관리  
서블릿 컨테이너는 서블릿의 탄생과 죽음을 관리한다.  
서블릿 클래스를 로딩하여 인스턴스화하고, 초기화 메서드를 호출하며 요청이 들어오면 적절한 서블릿 메서드를 호출한다.  
서블릿이 생명을 다하는 순간에는 적절하게 Garbage Collection을 진행하여 편의를 제공한다.

3. 멀티쓰레드 지원 및 관리  
서블릿 컨테이너는 요청이 올 때마다 새로운 자바 쓰레드를 생성한다.  
HTTP 서비스 메서드를 실행하고 나면, 쓰레드는 자동으로 죽게 된다.  
원래는 쓰레드를 관리해야 하나, 서버가 다중 쓰레드를 생성 및 운영해주어 안정성을 보장한다.

4. 선언적인 보안 관리  
서블릿 컨테이너를 사용하면 개발자는 보안에 관련된 내용을 서블릿 또는 자바 클래스에 구현하지 않아도 된다.  
일반적으로 보안관리는 XML배포 서술자에다가 기록한다.  
이는 보안에 대해 수정할 일이생겨도 자바 소스코드를 수정하여 다시 컴파일 하지 않아도 보안관리가 가능하다.

### **Servlet의 생명주기**
![](https://t1.daumcdn.net/cfile/tistory/991870335A04292F0B)  

1. 클라이언트의 요청이 들어오면 컨테이너는 해당 서블릿이 메모리에 있는지 확인하고, 없을 경우 init() 메서드를 호출하여 적재한다.   init() 메서드는 처음 한 번만 실행되기 때문에, 서블릿의 쓰레드에서 공통적으로 사용해야하는 것이 있다면 

2. init()이 호출된 후 클라이언트의 요청에 따라서 service() 메서드를 통해 요청에 대한 응답이 doGet()이 doPost()로 분기된다. 이때 서블릿 컨테이너가 클라이언트의 요청이 오면 가장 먼저 처리하는 과정으로 생성된 HttpServletRequest, HttpServletResponse에 의해 request와 response객체가 제공된다.

3. 컨테이너가 서블릿에 종료요청을 하면 destroy() 메서드가 호출되는데, 마찬가지로 한 번만 실행되며 종료시에 처리해야 하는 작업들을 destroy() 메서드를 오버라이딩하여 구현하면 된다.

## JSP(Java Server Page)
JSP를 요약하면 **Java 코드가 들어가 있는 HTML 코드**라고 할 수 있다.  
서블릿은 자바 소스코드 속에 HTML코드가 들어가는 형태인데, JSP는 이와 반대로 **HTML 소스코드 속에 자바 소스코드가 들어가는 구조**를 갖는 웹어플리케이션 프로그래밍 기술이다.  
HTML속에서 자바코드는 <% 소스코드 %> 또는 <%= 소스코드 =%>형태로 들어간다.  
자바 소스코드로 작성된 이 부분을 웹 브라우저로 보내는 것이 아니라 웹 서버에서 실행되는 부분이다.  
웹 프로그래머가 소스코드를 수정 할 경우에도 디자인 부분을 제외하고 자바 소스코드만 수정하면 되기에 효율성을 높여준다.  
또한 컴파일과 같은 과정을 할 필요없이 JSP를 작성하여 웹 서버의 디렉토리에 추가만 하면 사용이 가능하다.  
서블릿 규칙은 꽤나 복잡하여 JSP가 나오게 되었는데, JSP는 WAS(Web Application Server)에 의해서 서블릿 컨테이너로 변환하여 사용되어 진다.

### **JSP 동작 구조**
![screensh]( https://mblogthumb-phinf.pstatic.net/20150604_85/islove8587_1433408612779SkNsM_JPEG/4_JSP%C0%C7%B5%BF%C0%DB%B1%B8%C1%B6.jpg?type=w2)  
웹 서버가 사용자로부터 서블릿에 대한 요청을 받으면 서블릿 컨테이너에 그 요청을 넘긴다.  
요청받은 컨테이너는 HTTP Request와 HTTP Response 객체를 만들어, 이들을 통해 서블릿 doPost()나 doGet() 메서드 중 하나를 호출한다.  
만일 서블릿만 사용하여 사용자가 요청한 웹 페이지를 보여주려면 out 객체의 println 메서드를 사용하여 HTML 문서를 작성해야 하는데, 이는 추가/수정을 어렵게 하고 가독성도 떨어지기 때문에 JSP를 사용하여 비지니스 로직과 프레젠테이션 로직을 분리한다.  
여기서 서블릿은 데이터의 입력, 수정 등에 대한 제어를 JSP를 사용하여 프레젠테이션 로직을 수행하게 한 후 컨테이너에게 Response를 전달한다.  
이렇게 만들어진 결과물은 사용자가 해당 페이지를 요청하면 컴파일되어 자바 파일을 통해 .class파일이 만들어지고, 두 로직이 결합되어 클래스화 되는 것을 확인할 수 있다.  
즉, out객체의 println 메서드를 사용해서 구현해야 하는 번거로움을 JSP가 대신 수행해주는 것을 알 수 있다.