스프링 동작순서에 대해 공부했다.
스프링은 Filter - dispatch servlet - Interceptor - Argument Resolver - AOP - hadler method 순으로 값이 진행된다.

Servlet이란?

Dispatch Servlet이란?
예전에 JSP로 개발을 하면 Servlet을 생성하고 web.xml에 servlet에 대한 정보를 작성했었다.

예전에 군대에서 웹 개발할때 이렇게 했었는데 정말 귀찮은 작업이었다..ㅠ

하지만 Spring FrameWork가 나오고 Dispatch Servlet이 생기면서 web.xml을 작업하는게 사라졌다. Dispatch Servlet은 Front Controller라고 해서 서버에 요청이 들어오면 제일 앞에서 처리해주는 역할을 해준다.
