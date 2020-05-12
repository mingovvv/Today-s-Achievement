# LogBack 정리

#### Logback이란?

Logback은 Java에서 가장 많이 사용되었던 로깅 라이브러리인 log4j의 후속 버전이다. 
Logback은 log4j를 설계한 Ceki Gülcü에 의해 설계되었고 같은 개발자에 의해 개발되었다 보니 
logback을 사용하다보면 log4j를 사용하는 듯한 익숙함을 느낄 수 있다.

#### LogBack의 기능
 - Level 설정
    - 로그에 레벨을 설정할 수 있다. 각각의 로그에 레벨을 설정하고 설정파일에서 출력 로그 레벨을 설정하여 원하는 단계의 로그의
    레벨을 출력할 수 있다.
        1. ERROR : 일반 에러가 일어 났을 때 사용한다.
        2. WARN : 에러는 아니지만 주의할 필요가 있을 때 사용한다.
        3. INFO : 일반 정보를 나타낼 때 사용한다.
        4. DEBUG : 일반 정보를 상세히 나타낼 때 사용한다.
        5. TRACE : 경로추적을 위해 사용한다.
   
 - Appender
    - 출력 방법을 선택할 수 있다. 로그의 기록을 담당하는 Appender에게 출력위치(콘솔, 파일 등)나
    출력 내용(날짜/시간, 레벨, 스레드명 등)에 대한 패턴을 설정 할 수 있다.
    
 - Logger
    - 로그 마다 다른 설정내용을 쉽게 적용시킬 수 있습니다
위의 주요 설정을 포함한 다양한 설정 항목을 가지고 있는 객체(Logger)에 이름을 부여하여 필요한 상황에 맞게 적절한 Logger를 호출하여 사용할 수 있습니다.
그리고, LogBack이 특별하게 가지고 있는 기능도 있습니다.

#### LogBack 설정파일
Logback에서 설정파일을 작성하는 방법은 크게 두 가지가 있다.
 - XML을 이용한 설정방법 : logback.xml로 설정 파일 작성 후 해당 파일을 클래스패스에 위치시킨다.
 - Groovy 언어를 이용한 설정방법 : logback.groovy로 설정 파일 작성 후 해당 파일을 클래스패스에 위치시킨다.


## 출처
Link: [LogBack을 사용해야 하는 이유](https://beyondj2ee.wordpress.com/2012/11/09/logback-%EC%82%AC%EC%9A%A9%ED%95%B4%EC%95%BC-%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0-reasons-to-prefer-logback-over-log4j/)
