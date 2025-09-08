
## 기본적인 흐름

git add [파일명]으로 기록할 파일을 고름
git commit을 통해 git add로 고른 파일을 기록
- git commit -m 'message'를 통해 커밋에 메시지를 넣을 수 있음

이 때, add로 고른 파일을 임시로 모아두는 곳을 Staging Area,
파일을 기록한 것을 모아두는 곳을 Repository(저장소)라고 부름

때문에 git add는 스테이징한다라고도 함



## 유용한 명령어

- git add .
  - 현재 변경된 모든 파일을 스테이징
- git status
  - 현재 Staging Area에 존재하는 모든 변경 파일을 조회함
- git log --all --oneline
  - git log는 현재 체크아웃된 브랜치 기준으로 커밋 로그를 출력
  - --all은 모든 브랜치의 커밋 로그를 출력
  - --oneline은 커밋 로그를 한 줄씩 보여줌
  - --graph는 커밋 로그를 그래프로 그려줌
- git diff
  - 현재 파일과 직전 커밋을 비교
  - git difftool이 더 좋으니까 그거 쓰셈
    - git difftool 뒤에 커밋 아이디 붙이면 해당 커밋과 비교
    - 커밋 아이디를 두 개 붙이면 두 커밋을 비교
    - 요새 에디터 잘돼있는데 이딴거 왜씀? 그냥 에디터나 쓰셈 ㅅㄱ

수정하려고아무거나씀

vim에디터로 들어가면 j나 k로 위아래로 움직일 수 있음
q로 빠져나옴

## 브랜치

git branch [브랜치명]으로 브랜치를 생성
git switch [브랜치명]으로 해당 브랜치로 이동






