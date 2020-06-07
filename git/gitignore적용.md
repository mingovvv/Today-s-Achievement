# .gitignore
> git 버전 관리 시스템의 관리대상에서 제외할 파일 목록을 작성한다.  
> git이 해당 파일을 track하지 않게 됨.

#### .gitignore 설정
 - `.git` 파일이 있는 최상위 디렉토리에 생성
 - 파일명 `.gitignore`
 - 이미 버전 관리에 포함되어 있는 파일들을 `.gitignore`에 기록한다고 해서 버전 관리에서 제외하지 않는다.
 (한번 track한 파일은 지속적으로 track 한다.)
 
    -     [해결방안 - 원격저장소를 날리고 .gitignore를 다시 추가한다.]
          // 현재 Repository의 cache를 모두 삭제한다.
          $ git rm -r --cached .
          
          // [File Name]에 해당하는 파일을 원격 저장소에서 삭제한다.
          // (로컬 저장소에 있는 파일은 삭제하지 않는다.)
          $ git rm -r --cached [File Name]
          https://gmlwjd9405.github.io/2017/10/06/make-gitignore-file.html
 
#### .gitignore 작성 가이드
 - https://github.com/github/gitignore - 깃헙에서 제공해주는 `.gitignore`
 - https://www.toptal.com/developers/gitignore - 자신의 프로젝트에 맞는 `.gitignore` 세팅