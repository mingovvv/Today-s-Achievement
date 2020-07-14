# CROS 이슈

> 친한 동생이랑 토이프로젝트를 진행하고 있는데, 동생의 front단 서버에서 내가 작업하고 있는 back단 서버로 통신을 해보니 크롬에서 아래와 같은 error가 발생하고 데이터를 가져오지 못하는 이슈가 발생했다.

```
Access to XMLHttpRequest at 'http://{my-A-server-url}' from origin 'http://{my-B-server-url}' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource.
```

### 이슈 발생 배경

해당 이슈는 fornt단 'A' 서버에서 Ajax 통신으로 back단의 'B' 서버에 접근하면서 인터넷 브라우저(크롬) 웹 상에서 발생하였다.

### CORS?

CORS에 의한 블락이 되었다는 이야기인데, 우선 CORS에 대해 알아보자.

해당 error는 브라우저를 통해 발생했다!

**Cross-origin resource sharing**는 '다른 출처와의 자원의 공유'라는 의미인데 웹 페이지 상의 제한된 리소스를 최초 자원이 서비스된 도메인 밖의 다른 도메인에 대한 자원 공유 정책을 의미한다.

(여기서 출처 또는 도메인이 의미하는 것은 프로토콜 + 호스트 + 포트를 말한다.)

[##_Image|kage@qnVyX/btqFBfdfuaL/v3n2liQwYzkpVIFCKmdFmK/img.png|alignCenter|data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent"|출처에 따른&nbsp;||_##]

서로 다른 두 개의 어플리케이션이 소통하는 행위는 꽤나 위험한 환경을 의미하고, 그에 따른 공격 경로를 줄이기 위해 CORS같은 정책을 만들어 접근을 제한하고 있는 것이다. 

서버는 CORS를 위반하더라도 정상적으로 응답을 내려주고, 응답의 파기 여부는 브라우저가 결정한다.

출처

[https://developer.mozilla.org/ko/docs/Web/HTTP/CORS](https://developer.mozilla.org/ko/docs/Web/HTTP/CORS)
[https://evan-moon.github.io/2020/05/21/about-cors/](https://evan-moon.github.io/2020/05/21/about-cors/)