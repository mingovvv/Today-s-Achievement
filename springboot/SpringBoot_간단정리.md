# SpringBoot 간단 정리
> 스프링부트를 간단하게 정리해보자

`@SpringBootApplication`
 - `@SpringBootConfiguration` +`@ComponentScan` + `@EnableAutoConfiguration`
 
`@EnableAutoConfiguration`
 - 스프링부트 애플리케이션은 Bean을 두 번 등록한다.
    -   먼저 `@ComponentScan`을 통해 등록  
        (@Component를 가진 Class를 Bean으로 등록)
    -   그 후, `@EnableAutoConfiguration`을 통해 다시 등록
