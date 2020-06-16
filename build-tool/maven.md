# maven
> 빌드 툴

#### GOAL 이란?
 - maven의 작업 실행 단위를 일컫는 말. 체인 형태로 실행이 가능하다.

#### GOAL 의 종류
`mvn clean`
 - build를 하기전 build 결과를 비우는 명령어
 - `target` 디렉토리를 삭제
 
 `mvn compile`
 - compile 후 target 디렉토리가 생성되며 컴파일된 결과물이 만들어짐
 - 소스코드 컴파일, 리소스파일을 target/classes 디렉토리에 복사
 - target/classess
 
 `mvn test`
 - 유닛(단위) 테스트를 수행 하는 단계(테스트 실패시 빌드 실패로 처리, 스킵 가능)
 
 `mvn package`
 - compile 수행 후, 패키징 명령어
 - jar, war 등등의 파일 등의 배포를 위한 패키지로 만드는 단계
 
 `mvn install`
 - package 수행 후, package를 로컬 저장소에 설치하는 단계
 
 `mvn deploy`
 - 만들어진 package를 원격 저장소에 release하는 단계
 
 