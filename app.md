
## 기본적인 흐름

**git add [파일명]**으로 기록할 파일을 고름
**git commit**을 통해 git add로 고른 파일을 기록
- git commit -m '메세지'를 통해 커밋에 메시지를 넣을 수 있음

**이 때, add로 고른 파일을 임시로 모아두는 곳을 Staging Area, 파일을 기록한 것을 모아두는 곳을 Repository(저장소)라고 부름**

때문에 git add는 스테이징한다라고도 함

## 유용한 명령어

- **git add .**
  - 현재 변경된 모든 파일을 스테이징
- **git status**
  - 현재 Staging Area에 존재하는 모든 변경 파일을 조회함
- **git log --all --oneline**
  - git log는 현재 체크아웃된 브랜치 기준으로 커밋 로그를 출력
  - --all은 모든 브랜치의 커밋 로그를 출력
  - --oneline은 커밋 로그를 한 줄씩 보여줌
  - --graph는 커밋 로그를 그래프로 그려줌
- **git diff**
  - 현재 파일과 직전 커밋을 비교
  - git difftool이 더 좋으니까 그거 쓰셈
    - git difftool 뒤에 커밋 아이디 붙이면 해당 커밋과 비교
    - 커밋 아이디를 두 개 붙이면 두 커밋을 비교
    - 요새 에디터 잘돼있는데 이딴거 왜씀? 그냥 에디터나 쓰셈 ㅅㄱ

vim에디터로 들어가면 j나 k로 위아래로 움직일 수 있음

q로 빠져나옴

## 브랜치

**git branch [브랜치명]**으로 브랜치를 생성
**git switch [브랜치명]**으로 해당 브랜치로 이동

병합할 브랜치 중 기준이 될 브랜치로 스위치 후 git merge [합칠브랜치명] 입력하면 브랜치 병합 

이 때 두 브랜치가 동일한 코드 부분을 수정했을 경우 충돌이 일어나는데, 코드를 수정하고 git add & git commit하면 해결됨

#### merge의 종류

1. **3-way merge**
   - 각 브랜치에 신규 커밋이 1회 이상 있는 경우, 두 브랜치의 코드를 합쳐서 새로운 커밋을 생성함
   - 가장 기본적인 merge 방식
2. **fast-forward merge**
   - 병합 대상 브랜치에는 신규 커밋이 1회 이상 존재하나 기준 브랜치에는 신규 커밋이 없는 경우 병합 대상 브랜치를 기준 브랜치로 삼음
   - 이 경우 병합 대상 브랜치를 원래부터 main 브랜치였던 것으로 취급하므로 merge 커밋이 생기지 않음
     - 따라서 로그 상 브랜치가 나뉘지 않고 일직선처럼 보이게 되는데, 이렇게 로그의 복잡도를 줄이는 것을 **히스토리 직선화**라고 함
   - fast-forward merge일 경우라도 git merge --no-ff [브랜치명]을 입력하여 강제로 3-way merge할 수 있음
3. **rebase and merge**
   - rebase란 브랜치의 시작점을 다른 커밋으로 이동시키는 것을 의미함
   - rebase and merge는 브랜치의 시작점을 기준 브랜치의 최종 커밋으로 rebase 후 fast-forward merge하는 것을 의미함
     - 즉, 강제 fast-forward merge
   - 단, conflict가 발생할 가능성이 높으므로 신중히 해야 함
4. **squash and merge**
   - git merge [병합브랜치명] --squash로 실행
   - squash and merge는 병합 후 병합 대상 브랜치를 멸족시켜서 로그에 남기지 않음
   - rebase and merge와 비슷하게 로그를 줄일 수 있음

- rebase and merge 하는 법
  1. git switch [병합브랜치명]으로 병합브랜치로 이동
  2. git rebase [기준브랜치명]으로 기준브랜치의 최종 커밋으로 병합브랜치를 리베이스
     - 충돌할 경우 수정 후 git add & git rebase --continue
  3. git switch [기준브랜치명]으로 기준브랜치로 이동
  4. git merge [병합브랜치명]으로 병합(fast-forward merge)

- 병합이 완료된 브랜치는 git branch -d [삭제브랜치명]으로 삭제할 수 있음
  - 병합 후 브랜치는 보통 삭제하는 것이 일반적임
  - 병합하지 않은 브랜치는 git branch -D [삭제브랜치명]으로 삭제하면 됨


## 되돌리기

**git restore [파일명]**을 통해 해당 파일을 최종 커밋으로 되돌릴 수 있음
- 파일명 자리에 .을 입력하면 모든 파일이 최종 커밋으로 되돌아감
- git restore --source [커밋아이디] [파일명]을 통해 해당 파일을 특정 커밋으로 되돌릴 수 있음
- git restore --staged [파일명]을 통해 해당 파일의 스테이징을 취소할 수 있음

**git revert [커밋아이디]**를 통해 해당 커밋의 모든 변경을 취소할 수 있음
- git revert [커밋아이디1] [커밋아이디2]를 통해 여러 개의 커밋의 변경을 취소할 수 있음
- git revert HEAD를 통해 최종 커밋의 변경을 취소할 수 있음

**git reset [커밋아이디]**를 통해 커밋 헤드를 해당 커밋으로 이동
- git reset --soft [커밋아이디]를 통해 헤드 커밋 이후의 변경사항을 스테이징. working directory에는 영향이 없음
- git reset --mixed [커밋아이디]를 통해 헤드 커밋 이후의 커밋 변경사항을 working directory에 남김(기본값)
- git reset --hard [커밋아이디]를 통해 헤드 커밋 이후의 커밋 변경사항을 모두 삭제


# github 사용법

**git push [원격레포주소] [브랜치명]**으로 원격 저장소에 변경사항 저장
- -u를 입력하면 원격 저장소 주소와 브랜치를 기억하여 git push만으로 해당 저장소 브랜치에 변경사항을 저장함
**git remote add [변수명] [원격레포주소]**를 통해 원격 저장소의 주소를 변수에 저장할 수 있음

## 협업

**git clone [원격레포주소]**를 입력하면 원격 저장소의 현재 파일들을 내려받음

다른 팀원이 이미 push하여 현재 로컬 저장소와 원격 저장소 간 차이가 발생할 경우 push가 불가능해짐
이 경우 git pull [원격레포주소] [브랜치명]을 통해 로컬 저장소에 원격 저장소의 신규 커밋을 덮어씌워야 push할 수 있음

git pull은 git fetch + git merge를 합친 것
- git fetch는 원격 저장소의 신규 커밋들을 가져옴
- git merge가 포함되어 있는 탓에 conflict가 발생할 수도 있음

.gitignore 파일에 커밋할 필요가 없는 파일을 명시할 수 있음
명시된 파일들은 스테이징 대상이 되지 않음