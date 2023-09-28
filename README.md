# SpringMVC <br>

<br>

## 1. Servlet <br>

<h4>● @WebServlet 애노테이션을 사용하여 서블릿의 이름과 url을 매핑할 수 있음</h4>
<br>
<h3>●서블릿 컨테이너 동작 방식</h3>

<br>
<h4> 톰캣의 서블릿 생성 과정: 스프링 부트 -> 톰캣 서버 -> 서블릿 생성 </h4>
<h4> 요청&응답 메시지 구조: http request 생성 -> 서블릿 실행 -> 서블릿 종료 -> http response 생성 </h4>

<h5>http 요청 메시지에는 start line(http 메소드,url,쿼리 등), 헤더, (메시지)바디가 포함되어 있으며, HttpServletRequest 객체가 이를 지원함</h5>
<h5>HttpServletRequest는 그외 local 정보 등 기타 정보도 제공함</h5>
<h5>HttpServletResponse는 http 응답코드 지정, 헤더, 바디를 생성하며, content-type, 쿠키, 리다이렉트 같은 편의 기능도 제공함</h5>
<br>

<h3>●HTTP 요청 데이터</h3>
<br>
<h4>1. Get- 쿼리 파라미터: 메시지 바디 없이 URL의 쿼리 파라미터에 데이터를 전달하는 방식</h4>
<h4>2. POST- HTML FORM: 메시지 바디에 쿼리 파리미터 형식으로 데이터를 전달하는 방식</h4>
<h4>3. Http meesage body: 데이터를 직접 담아서 요청하는 방식으로 Http API에서 주로 사용 하며 주로 JSON을 사용하여 통신함</h4>

<br>

<h3>●HTTP 응답 데이터</h3>
<br>
<h4>1. 단순 텍스트</h4>
<h4>2. HTML: content-type을 text/html으로 지정 필요</h4>
<h4>3. Http API: Message Body에 JSON을 사용하여 응답하며 content-type을 application/json으로 지정 필요</h4>
<br>
<hr>

## 2. MVC 패턴 <br>
<h4>●서블릿을 이용하여 웹 App 구현 </h4>
<br>
<h5>자바 코드로 HTML Form을 직접 만들어 제공해야 함</h5>
<h5>자바 로직 작동 후 HTML을 동적으로 생성 및 응답</h5>
<h5>이는 비효율적인 행위이자 템플릿 엔진이 나온 이유</h5>

<br>
<h4>●JSP를 이용하여 웹 App 구현 </h4>
<br>
<h5>JSP 이용 시 추가 라이브러리 필요</h5>
<h5>뷰 화면을 구성하는 HTML을 작성하는 작업 용이</h5>
<h5>다른 템플릿 엔진에 밀려 사장되는 추세</h5>

<br>
<h3>●서블릿과 JSP의 한계</h3>
<br>
<h5>서블릿: 지저분하고 복잡한 HTML 코드와 이를 직접 만듦으로 비효율적</h5>
<h5>JSP: 뷰 영역과 로직 영역이 함께 있어 유지보수가 어려우며 보안 문제가 존재</h5>
<br>

<h4>●MVC를 이용하여 웹 App 구현</h4>
<h5>변경의 라이프 사이클: UI의 수정과 비즈니스 로직의 수정은 서로 영향을 주지 않아야 함. 즉, 변경 주기가 다르면 분리해야 함</h5>
<br>
<h5>Controller: 비즈니스 로직을 실행 & view가 읽을 데이터를 모델에 전달</h5>
<h5>Model: 뷰에 출력할 데이터를 담아 둠, 컨틀롤러와 뷰 사이의 매개체</h5>
<h5>View: 모델에 담겨 있는 데이터를 화면에 출력 & HTML 생성</h5>
<br>
<h5>작동 과정</h5>
<h6>Controller가 서비스 or 레포지토리를 호출하여 비지니스 로직 수행</h6>
<h6>Model에 해당 데이터 전달 & Model이 데이터 읽음</h6>
<h6>Controller가 View에게 신호하여 View가 Model을 받아옴</h6>
<h6>View가 Model의 데이터를 참고하여 화면에 View를 보여줌(HTML 생성)</h6>
<br>
<h4>특징</h4>
<br>
<h5>/WEB-INF: 해당 경로 안에 view 파일 생성 시 외부에서 호출 불가능 -> 컨트롤러를 통해서 호출하기 위함</h5>
<h5>컨트롤러 로직과 뷰 로직을 확실히 분리 가능 -> 유지보수 효율성 향상</h5>
<h5>컨트롤러에서 뷰로 이동 시 디스패처(dispatcher)를 사용함</h5>

<br>
<h3>●MVC패턴 한계</h3>
<br>
<h5>포워드 중복: 반복된 코드 작성</h5>
<h5>viewPath 중복: 다른 view로 바꾸기 위해서는 전체 코드 수정 필요</h5>
<h5>사용하지 않는 코드: response 객체와 같은 코드는 사용하지 않음</h5>
<h5>어려운 공통 처리: 컨트롤러 호출 전에 이를 해결하기 위한 역할 필요 -> 프론트 컨트롤러</h5>
<hr>

## 3. MVC 프레임워크 <br>
<h4>●FrontController 패턴 </h4>
<br>
<h5>공통로직을 처리하는 하나의 서블릿을 구현한 컨트롤러</h5>
<h5>나머지 컨트롤러는 서블릿 필요X</h5>
<h5>스프링 웹 MVC의 DispatcherServlet</h5>
<br>

<h4>●1. FronController 도입</h4>
<br>
<h5>기존 코드는 최대한 유지한 채로 공통로직을 처리하는 컨트롤러 구현</h5>
<h5>URI 매핑을 통해 존재하지 않으면 404 상태 코드 반환</h5>

<br>
<h4>●2. View 분리</h4>
<br>
<h5>컨트롤러에서 뷰로 이동하는 중복 코드를 객체로 분리</h5>
<h5>객체 생성 시 해당 경로에 해당하는 URI로 이동</h5>
<br>
<h4>●3. Model 추가</h4>
<br>
<h5>필요 없는 request,response 객체 제거 -> 서블릿 종속성 제거</h5>
<h5>별도의 Model 객체 반환을 위한 ModelView 객체 생성</h5>
<h5>뷰의 논리 이름을 반환하기 위한 viewResolver 호출</h5>
<h5>뷰 리졸버는 논리 뷰 이름을 실제 물리 뷰 경로로 변경 후 MyView 객체 반환 </h5>
<br>
<h4>●4. 단순하고 실용적인 컨트롤러</h4>
<br>
<h5>기존 V3에서 ViewName만 반환</h5>
<h5>model 객체는 파라미터로 전달받아 사용, 직접 생성 필요 X </h5>
<h5>개발자의 개발 편의성 증가</h5>
<br>
<h4>●5. 유연한 컨트롤러</h4>
<br>
<h5>어댑터 패턴: 프론트 컨트롤러가 다양한 방식의 컨트롤러 처리가 가능 </h5>
<h5>기존 구조에 핸들러 어댑터와 핸들러(컨트롤러)를 추가 </h5>
<h5>반환 타입이 다르다면 어댑터가 이를 형식을 맞춰서 반환</h5>

<hr>

## 4. Spring MVC 구조 이해 <br>

<h4>●직접 만든 프레임워크 = Spring MVC </h4>
<h5>Front Controller -> Dispatcher Servlet</h5>
<h5>Dispatcher Servlet에서 doDispatch를 호출하여 작동</h5>

<br>
<h4>●동작 순서 </h4>
<h5>1. 핸들러 조회: 핸들러 매핑을 통해 URL에 매핑된 핸들러 조회 </h5>
<h5>2. 핸들러 어댑터 조회: 핸들러를 실행할 수 있는 어댑터 조회 </h5>
<h5>3. 핸들러 어댑터 실행 후 핸들러 실행 </h5>
<h5>4. ModelAndView 반환: 핸들러 반환 정보를 ModelAndView로 변환하여 반환 </h5>
<h5>5. 뷰 리졸버 호출: 뷰 리졸버를 통해 뷰를 찾은 후 이를 반환 </h5>
<h5>6. view 렌더링</h5>
<br>

<h4>●특징</h4>
<h5>ModelAndView가 아닌 String을 반환하여도 view로 인식 가능 </h5>
<h5>Model 파라미터를 이용 & 뷰의 논리 이름 직접 반환 가능 </h5>
<h5>@RequestParam을 사용하여 요청 파라미터를 받음 </h5>
<br>

<h4>●@RequestMapping</h4>
<h5>RequestMappingHandlerMapping은 @RequestMapping or @Controller가 클래스 레벨에 있다면 매핑 정보로 인식</h5>
<h5>가장 우선순위가 높은 핸들러 매핑과 핸들러 어댑터 보유 </h5>
<h5>실무에서 99.9% 이상 이 방식의 컨트롤러를 사용 </h5>
<h5>요청 정보를 매핑한 후 해당 URL 호출 시 이 메서드가 호출되며 메서드 이름은 상관 X </h5>
<h5>메서드 단위이므로 컨트롤러 클래스의 통합 및 조합 가능 </h5>
<h5>Http Method도 함께 구분 가능 </h5>
<br>

<h4>●@Controller</h4>
<h5>스프링이 자동으로 스프링 빈으로 등록함 </h5>
<h5>스프링 MVC에서 애노테이션 기반 컨트롤러로 인식 </h5>
<hr>
