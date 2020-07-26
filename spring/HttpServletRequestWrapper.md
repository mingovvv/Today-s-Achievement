#HttpServletRequestWrapper
> HttpServletRequestWrapper, HttpServletResponseWrapper

`HttpServletRequest`, `HttpServletResponse` 객체의 Stream은 한번 읽히면 내부적으로 다시 읽지 못하도록
막혀있다. 로깅처리를 위해 `HttpServletRequest`, `HttpServletResponse` 객체의 Stream을 받아 특정 로직을 구현하면
Controller단에서 `Request`, `Response` 데이터를 바인딩 할 수 없다.
그 후 `has already been called for this` 라는 오류 메시지가 출력된다.

```
java.lang.IllegalStateException: getReader() has already been called for this request
org.springframework.http.converter.HttpMessageNotReadableException: Could not read JSON: Stream closed; nested exception is java.io.IOException: Stream closed
```

#### 해결방안
해결방안으로는 `HttpServletRequestWrapper`, `HttpServletResponseWrapper` 클래스를 구현하는 것이다.
Filter 계층에서 `HttpRequest를` `HttpServletWrapper에게` 넘겨주고 `Wrapper` 클래스 내부에서 Stream을 복사해서
새 Stream을 만들어 사용하는 것이다.

*spring의 interceptor 계층에서는 call by value에 의해 처리가 불가하다. 

#### 출처
https://meetup.toast.com/posts/44 