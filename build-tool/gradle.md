# gradle
> 오픈 소스 빌드 도구, 그루비로 작성되어 DSL(Domain-Specific Language)스크립트를 사용한다.

#### gradle 설정파일 
 - `.gradlew`
    - 리눅스 계열 실행파일
 - `.gradlew.bat`
    - 윈도우 계열 실행파일
 - `.gradle` 파일
    - Task로 생성된 파일
 - `gradle` 폴더
    - wrapper 파일이 저장되어 있는 폴더
 - `.src` 파일
    - 소스 코드 파일, 리소스 파일 등 프로젝트와 관련된 파일
 - `main` 폴더
   - java 소스 코드를 넣어두기 위한 폴더
 - `test` 폴더
   - 단위 테스트 파일을 모아두는 폴더
 - `settings.gradle`
    - 프로젝트에 대한 설정 정보를 작성한 파일
 - `build.gradle`
    - Groovy 언어로 작성됨
    - Maven의 pom.xml과 같은 역할을 수행

#### gradle로 profile을 구분짓는 방법
 - default profile 속성은 'dev'가 된다.
 - 실행 -Pprofile=qa
    - qa 인자를 넘긴다는 것
  
    
    ext.profile = (!project.hasProperty('profile') || !profile) ? 'dev' : profile
    
    sourceSets {
    	main {
    		resources {
    			srcDirs "src/main/resources", "src/main/resources-env/${profile}"
    		}
    	}
    }

#### gradle이 maven보다 많이 쓰이는 이유?
 - 단순하다. 더 빠르다.
   - https://www.holaxprogramming.com/2017/07/04/devops-gradle-is-faster-than-maven/
   
#### gradle task

#### gradle plugin
 - implementation
    -   Gradle이 컴파일 클래스 경로에 종속 항목을 추가하고 빌드 출력에 종속 항목을 패키징한다. 
        그러나 모듈에서 implementation 종속 항목을 구성하면 모듈이 컴파일 시간에 
        종속 항목을 다른 모듈에 누출하기를 바라지 않는다는 것을 Gradle에 알려주는 것이다.
        즉, 종속 항목은 런타임에만 다른 모듈에서 이용할 수 있다.
        api 또는 compile(지원 중단됨) 대신 이 종속 항목 구성을 사용하면 빌드 시스템에서 
        다시 컴파일해야 하는 모듈 수가 줄어들기 때문에 빌드 시간이 크게 개선될 수 있다. 
        예를 들어 implementation 종속 항목이 API를 변경하면 
        Gradle은 이 종속 항목과 이에 직접적으로 종속된 모듈만 다시 컴파일한다.
        대부분의 앱과 테스트 모듈은 이 구성을 사용해야 한다.
        
 - api
    -   Gradle은 컴파일 클래스 경로와 빌드 출력에 종속 항목을 추가한다. 
        모듈에 api 종속 항목이 포함되면 모듈이 다른 모듈로 종속 항목을 이전하여 
        다른 모듈에서 런타임과 컴파일 시간에 사용할 수 있도록 한다는 것을 Gradle에 알려주는 것이다.
        이 구성은 compile(현재는 지원 중단됨)처럼 작동하지만 주의해서 
        다른 업스트림 소비자에게 이전해야 하는 종속 항목과 사용해야 한다. 
        그 이유는 api 종속 항목이 외부 API를 변경하면 Gradle이 컴파일 시 
        종속 항목에 액세스 권한이 있는 모든 모듈을 다시 컴파일하기 때문입니다. 
        따라서 api 종속 항목 수가 많으면 빌드 시간이 크게 증가할 수 있습니다. 
        종속 항목의 API를 별도의 모듈에 노출하지 않으려면 라이브러리 모듈에서 
        implementation 종속 항목을 대신 사용해야 한다.
        
 - compileOnly
    -   Gradle은 컴파일 클래스 경로에만 종속 항목을 추가한다.(즉 빌드 출력에는 추가되지 않음). 
        컴파일하는 동안 종속 항목이 필요한 경우 유용하지만 런타임에 이를 표시하는 것은 선택사항이다.
        이 구성을 사용하는 경우 라이브러리 모듈에 런타임 조건을 포함하여 
        종속 항목을 사용할 수 있는지 확인한 다음 종속 항목이 제공되지 않는 경우에도 
        작동할 수 있도록 동작을 적절하게 변경해야 한다. 이 방법은 중요하지 않은 일시적인 종속 항목을 
        추가하지 않으므로 최종 APK의 크기를 줄이는 데 도움이 된다. 
        이 구성은 provided(현재는 지원 중단됨)와 동일하게 작동한다.
        
        참고: compileOnly 구성은 AAR 종속 항목과 함께 사용할 수 없다.
 - runtimeOnly
    -   Gradle은 런타임 동안 사용하기 위해 빌드 출력에만 종속 항목을 추가한다. 
        즉 컴파일 클래스 경로에는 추가되지 않는다. 
        이 구성은 apk(현재는 지원 중단됨)와 동일하게 동작한다.
        
 - annotationProcessor
    -   주석 프로세서인 라이브러리에 종속 항목을 추가하려면 annotationProcessor 구성을 사용하여 
        주석 프로세서 클래스 경로에 추가해야 한다. 
        이 구성을 사용하면 컴파일 클래스 경로를 주석 프로세서 클래스 경로에서 분리하여 빌드 성능이 개선되기 때문입니다. Gradle은 컴파일 클래스 경로에서 주석 프로세서를 찾으면 컴파일 회피를 비활성화하며 이는 빌드 시간에 부정적인 영향을 미친다
        (Gradle 5.0 이상에서는 컴파일 클래스 경로에서 발견된 주석 프로세서를 무시)
    
#### 출처
https://developer.android.com/studio/build/dependencies?utm_source=android-studio#dependency_configurations

 