# Retrofit2
> 레트로핏은 Square사에서 제공하는 오픈소스 라이브러리로서, 서버와 REST API를 통한 통신을 도와주는 역할을 수행.  
> 자바와 안드로이드 진영에서 많이 사용되고 있는 추세.

#### 특징
 - 기본적으로 OkHttp를 네트워킹 계층으로 활용한다.
 - `GET`, `POST`, `PUT`, `PATCH`, `DELETE` 등의 http 메소드 사용가능
 - 객체는 `Retrofit` instance 에 지정된 converter에 따라 변환
 
 #### 사용법
  - interface 영역
  -     public interface GitHubService {
          @GET("users/{user}/repos")
          Call<List<Repo>> listRepos(@Path("user") String user);
        }
  - class  영역
  -     Retrofit retrofit = new Retrofit.Builder()
            .baseUrl("https://api.github.com/")
            .build();
        
        GitHubService service = retrofit.create(GitHubService.class);
   - call 영역
   -     Call<List<Repo>> repos = service.listRepos("octocat");
   
#### SYNCHRONOUS vs ASYNCHRONOUS
  - `call` instance는 동기적 또는 비동기적으로 실행할 수 있음
  - 
  
#### Converter 종류
    Gson: com.squareup.retrofit2:converter-gson
    Jackson: com.squareup.retrofit2:converter-jackson
    Moshi: com.squareup.retrofit2:converter-moshi
    Protobuf: com.squareup.retrofit2:converter-protobuf
    Wire: com.squareup.retrofit2:converter-wire
    Simple XML: com.squareup.retrofit2:converter-simplexml
    JAXB: com.squareup.retrofit2:converter-jaxb
    Scalars (primitives, boxed, and String): com.squareup.retrofit2:converter-scalars
    
 