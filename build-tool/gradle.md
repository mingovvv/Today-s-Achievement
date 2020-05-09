gradle
오픈 소스 빌드 도구
기본 Maven과 Ivy repository를 사용한다.


빌드 후 생성 되는 파일
.gradlew
 - 리눅스 계열 실행파일
.gradlew.bat
 - 윈도우 계열 실행파일
.gradle 파일
 - Task로 생성된 파일
gradle 파일
 - wrapper 파일이 저장되어 있는 폴더
.src 파일
 - 소스 코드 파일, 리소스 파일 등 프로젝트와 관련된 파일
 - main 폴더
   - java 소스 코드를 넣어두기 위한 폴더
 - test 폴더
   - 단위 테스트 파일을 모아두는 폴더
settings.gradle
 - 프로젝트에 대한 설정 정보를 작성한 파일
build.gradle
 - Groovy 언어로 작성됨
 - Maven의 pom.xml과 같은 역할을 수행

gradle로 profile을 구분짓는 방법
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

gradle이 maven보다 많이 쓰이는 이유?
 - 단순하다. 더 빠르다.
   - https://www.holaxprogramming.com/2017/07/04/devops-gradle-is-faster-than-maven/
 