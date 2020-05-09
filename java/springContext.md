# spring context
> Root WebApplicationContext와 Servlet WebApplicationContext에 대해 간단하게 정리해보자.

### Root WebApplicationContext
 - ContextLoaderListener 에 의해서 생성된다.
 - Root에 등록된 Bean은 모든 Context에서 사용되어 있다.(공유) 
 
### Servlet WebApplicationContext 
 - DispatcherServlet 에 의해서 생성된다.
 - Servlet에 등록된 Bean은 오직 Servlet Context에서만 사용된다.
 
 
 