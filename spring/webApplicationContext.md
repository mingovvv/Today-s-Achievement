# WebApplicationContext

![이미지 이름](https://docs.spring.io/spring/docs/current/spring-framework-reference/images/mvc-context-hierarchy.png)

스프링에서 context 계층 관계는 흔히 부모-자식 관계로 이루어진다. 
위 그림처럼 servlet-context가 root-context를 참조하는 관계이며, 그 반대는 불가능하다.
  
##### Servlet WebApplicationContext
 -     <servlet>
           <servlet-name>dispatcherServlet</servlet-name>
           <servler-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
           <init-param>
               <param-name>contextConfigLocation</param-name>
               <param-value>/WEB-INF/spring-servlet.xml</param-value>
           </init-param>
           <load-on-startup>1</load-on-startup>
       </servlet>

   - DispatcherServlet을 통해 생성되며 해당 servlet에서만 사용가능한 컨텍스트가 된다.
   - web application에서 client의 reqeust를 받는 entry point의 역할이므로 요청에 대한 처리를 위해 
   Controller(handler mapping), View(view resolver)등 의 설정을 담당한다.
   - 
   
 
##### Root WebApplicationContext
 -      <context-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>/WEB-INF/conf/root-context.xml</param-value>
        </context-param>
        <listener>
            <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
        </listener>
   - ContextLoaderListner를 통해 생성되며 전역에서 사용가능한 컨텍스트가 된다.
   - 실제 비지니스 로직을 위한 service layer와 해당 service layer에서 조회 및 처리에 필요한 
   database 와 연결되는 repository layer를 구성하는 bean들에 대한 설정을 담당한다.

> 두 종류의 컨텍스트는 `<param-name>`이 contextConfigLocation로 동일한 것을 확인할 수 있는데, 이로 인해 컨텍스트간의
>계층 관계를 연결해주는 것이다. 

`<component-scan/>` 을 통한 각 context에 대한 bean 등록시 exclude, include를 적절히 활용하여 
불필요한 중복 bean등록이 되지 않도록 해주는 것이 좋다. 또한, 같은 맥락에서 트랜젝션 제어를 위한 
`<annotation-driven/>` 설정도 트랜젝션을 제어하고자 하는 해당 bean이 등록된 context에 선언을 해 주어야 
하는것도 잊지 말자.

    <!-- # Servlet WebApplicationContext -->
    <context:component-scan base-package="com.devyu.*.controller" use-default-filters="false">
        <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
    </context:component-scan>
---
    <!-- # Root WebApplicationContext -->
    <context:component-scan base-package="com.devyu">
        <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
    </context:component-scan>
  
