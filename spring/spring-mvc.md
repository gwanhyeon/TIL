# spring mvc 동작 과정

1. 클라이언트가 서버에 Request를 하면 스프링에서 제공하는 DispatcherServlet 이라는 클래스가 요청을 가로챈다.
web.xml에 모든 url에 서블릿 매핑을 하여 모든 요청을 DispatcherServlet이 가로챌 수 있게 변경 가능하다.

2. 요청을 가로챈 DispatcherServlet은 HandlerMapping에게 어떤 컨트롤러에게 요청을 위임하면 좋을지 물어본다.
(servlet-context.xml)에서 등록된 @Controller 컴포넌트 스캔을 통하여 어느 컨트롤러에게 요청을 위임처리 할지 확인이 가능하다. 요청 처리할 컨트롤러 빈 객체를 DispatcherServlet에 다시 전달한다.

3. DispatcherServlet은 HandlerAdapter 빈에게 요청 처리를 위임한다.

4. 컨트롤러에서는 Service를 DI 받아 비즈니스로직을 Service에게 위임한다.

5. service에서는 요청에 필요한 작업을 담당하며 데이터베이스에 접근이 필요하면 DAO를 주입받아 DB처리는 DAO에게 위임한다.

6. DAO SQL 쿼리를 날려 DB에 저장되어있는 정보를 받아 서비스에게 다시 돌려준다. DTO 객체 @RequestParam, @RequestBody 로 부터 DB 조회에 필요한 데이터를 받아와 쿼리를 만들어 보내고, 결과로 받은 Entity 객체를 가지고 Response에 필요한 DTO객체로 변환한다.

7. 모든 비즈니스 로직을 끝낸 서비스가 결과물을 컨트롤러에게 넘긴다.

8. HandlerAdapter는 컨트롤러의 처리 결과를 ModelAndView라는 객체로 변환해서 DispatcherServlet에 넘긴다.

9. DispatcherServlet은 ViewResolver에게 받은 뷰의 대한 정보를 넘긴다.

10. ViewResolver는 해당 JSP를 찾아서 뷰 DispatcherServlet에게 알려준다. 응답을 생성하기 위해 JSP를 사용하는 ViewResolver는 매번 새로운 View객체를 생성해서 DispatcherServlet에 반환한다.

11. DispatcherServlet은 ViewResolver로부터 받은 응답을 위한 View객체에게 Render를 지시하고 View객체는 응답 로직을 처리한다.

12.JSP를 사용하는 경우 View객체는 JSP를 실행하므로서 웹 브라우저에 전송할 응답 결과를 생성하고 이로써 모든 과정이 끝난다. 결과적으로 DispatcherServlet이 클라이언트에게 렌더링된 View를 응답한다.
