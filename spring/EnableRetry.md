# @EnableRetry
> 특정 Exception이 발생했을 경우 일정 횟수만큼 재시도할수 있는 애노테이션  
> 현업에서 유용하게 사용중(따봉)

```
@SpringBootApplication
@EnableRetry // 추가
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

```
// retry 의존성 
compile group: 'org.springframework.retry', name: 'spring-retry', version: '1.3.0'
compile 'org.springframework.boot:spring-boot-starter-aop' // aop 사용됨
```

#### 사용법
```
@RestController
public class Controller {

    @GetMapping(value = "/test")
    @Retryable(include = Exception.class, maxAttempts = 4) // 반복할 메소드에 설정
    public String getName() throws Exception {
        int i = 0;
        if(i == 3) {
            System.out.println("성공");
        } else {
            i++;
            System.out.println("실패");
            throw new Exception();
        }
        return "테스트";
    }

    @Recover
    public String recover(Exception e) {
        // maxAttempts 이후 호출되는 메소드
    }
}
```
우선 위의 예제로 만든 메서드는 무조건 실패만 출력된다. retry로 재시작되어도 i값이 0으로 초기화 되기 때문 ㅎㅎ.. (수정하기
귀찮으니 사용법만 봤으면 됐당.)  
  
`@Retryable`의 속성값
 1. include - 다시시작하기 위해 매칭되길 원하는 예외
 2. exclude - 제외되길 원하는 예외
 3. maxAttempts - 해당 예외 발생시, 재시도 횟수(default : 3회)
 4. backoff - 재시도 pause 시간(default : 1초)


