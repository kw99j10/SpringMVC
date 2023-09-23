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
