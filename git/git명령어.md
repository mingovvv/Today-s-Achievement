# git 명령어
> 기존에 자주 사용하는 명령어를 제외한 git의 명령어 정리

#### git stash
`git stash`는 commit을 하지 않고 다른 branch로 이동할 때 마무리하지 않은 작업을
스택에 잠시 저장할 수 있도록 하는 명령어. 일종의 `책갈피` 역할.  
Modified이면서 Tracked 상태인 파일을 저장한다.

 - `git stash`
    -   stash 추가하기
 - `git stash list`
    -   stash 목록 확인하기
 - `git stash apply [stash 이름]`
    -   stash 적용하기(stash 이름을 적지 않으면 가장 최근 stash를 적용한다.)
 - `git stash apply --index`
    -   stash를 적용하면 staged였던 파일을 unstarged 상태로 변경하면서 불러온다.
    -   `--index` 옵션을 추가하면 staged 상태까지 복원한다.
 - `git stash drop [stash 이름]`
    -   스택에 남아있는 stash를 제거(stash 이름을 적지 않으면 가장 최근 stash를 제거한다.)
 - `git stash pop`
    -   적용과 동시에 스택에서 해당 stash를 제거한다.
 -  `git stash show -p [stash 이름] | git apply -R`
    -   실수로 stash를 적용한 것을 되돌린다.
