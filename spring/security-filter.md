## 오늘 찾아보 링크 목록

1. [spring security filter](https://gaebalsogi.tistory.com/53)

## 공부한 내용

### Spring Security Filter 구조에 대해 공부

오늘은 Spring Security Filter에 대해서 공부했다.

클라이언트가 애플리케이션에 요청 메시지를 보내면 컨테이너는 요청 URI의 경로를 기반으로
HttpServletRequest를 처리해야 하는 필터와 서블릿을 포함한 FilterChain을 생성한다.
여기서 서블릿은 DispatcherServlet을 말한다.

스프링은 서블릿 컨테이너의 생명주기와 스프링의 ApplicationContext 사이를 이어주는 DelegatingFilterProxy라는 이름의 필터 구현체를 제공한다.
서블릿 컨테이너는 자체 표준에 의해 필터를 등록하는데, 스프링에 의해 정의된 빈들은 인식하지 못한다.
DelegatingFilterProxy는 서블릿 표준 메커니즘에 의해 등록될 수 있지만 필터를 구현하는 모든 작업을 스프링 빈에 위임한다

스프링 시큐리티가 제공하는 서블릿에 대한 지원은 FilterChainProxy내에 포함된다.
FilterChainProxy는 스프링 시큐리티에서 제공하는 특수한 필터로 SecurityFilterChain을 통해 많은 필터 인스턴스에 역할을 위임할 수 있다.
FilterChainProxy는 빈이기 때문에 주로 DelegatingFilterProxy에 의해 wrapping 된다.
