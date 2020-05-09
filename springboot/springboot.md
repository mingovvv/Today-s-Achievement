springboot

WAR 배포
 - SpringBootServletInitializer를 상속
 - servlet 3.0 스펙에 새로운 기능 중 하나는 web.xml 없이 배포가 가능한 점
 - Apache Tomcat의 경우 7.0 버전 부터 Servlet 3.0을 지원한다.
 - SpringBootServletInitializer
 - servelt 3.0 이상 사용시, WebApplicationInitializer 인터페이스를 구현하면 스프링 프레임워크에서 web.xml을 대신할 수 있다.
 -     public class MyWebAppInitializer implements WebApplicationInitializer {
       @Override
           public void onStartup(ServletContext container) {
             // Create the 'root' Spring application context
             AnnotationConfigWebApplicationContext rootContext =
               new AnnotationConfigWebApplicationContext();
             rootContext.register(AppConfig.class);
       // Manage the lifecycle of the root application context
             container.addListener(new ContextLoaderListener(rootContext));
       // Create the dispatcher servlet's Spring application context
             AnnotationConfigWebApplicationContext dispatcherContext =
               new AnnotationConfigWebApplicationContext();
             dispatcherContext.register(DispatcherConfig.class);
       // Register and map the dispatcher servlet
             ServletRegistration.Dynamic dispatcher =
               container.addServlet("dispatcher", new DispatcherServlet(dispatcherContext));
             dispatcher.setLoadOnStartup(1);
             dispatcher.addMapping("/");
           }
       }
 - SpringBootServletInitializer는 WebApplicationInitializer 인터페이스의 구현체
 - 
 
 
 링크
 - https://medium.com/@SlackBeck/spring-boot-%EC%9B%B9-%EC%95%A0%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98%EC%9D%84-war%EB%A1%9C-%EB%B0%B0%ED%8F%AC%ED%95%A0-%EB%95%8C-%EC%99%9C-springbootservletinitializer%EB%A5%BC-%EC%83%81%EC%86%8D%ED%95%B4%EC%95%BC-%ED%95%98%EB%8A%94%EA%B1%B8%EA%B9%8C-a07b6fdfbbde