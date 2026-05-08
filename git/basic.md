

# Git의 목적

개발을 하거나 운영할 때 이전 버전이 필요하거나 언제든지 특정 시점으로 되돌릴 수 있어야한다.
누가, 언제, 어떤 내용을 변경했는지 추적되어야한다.
언제든지 과거 버전으로 되돌릴 수 있다.
그리고 동시 작업해도 덮어씌움이 없어야함. -> 최신상태에서 작업하도록 설계됨



# git 기본 흐름

github에서 가져오기 or 로컬에서 git 입히기 -> "/opt/app" 작업완료! -> 담기(임시저장) -> 확정(고유ID생성) -> github 전송

1. github에서 가져오기 = git clone [리포지토리 주소]
   로컬에서 git 입히기 = git init

   디렉토리에서 git으로 관리하기 위해서 .git 숨김파일이 존재해야한다.
   .git에 파일의 히스토리 기록됨
   git init으로 로컬에서 생성할 수 있으며 github와 동기화하면된다.
   git clone으로 가져오면 자동 생성된다.
   
   
2. 담기 = git add [파일명]
   .git/objects -> 새 버전 파일 내용물을 해시값으로 기록 #해시값1, 과거의 모든 커밋이 저장되어있음
   .git/index -> 실제 파일이름과 object의 해시값을 매핑


3. 확정(고유ID생성) = git commit -m [버전 설명 메세지]
   임시저장된 버전을 특정 버전으로 이름을 붙여 확정 = 커밋 생성
   .git/objects -> 새 버전 메세지, 날짜 등을 기록한 파일을 해시값으로 기록 #해시값2
   .git/refs/heads/main ->  해시값2를 덮어씀, main이 되는 것(최신커밋)


4. github 전송
   git push



# Git 명령어

기본
## git clone 최초 복사
## git pull 최신 동기화
## git add . 파일 담기
## git commit -m 확정
## git push 전송
## git status 상태확인
## git log (--oneline) 기록확인
## git checkout [고유ID] 과거 버전 내용 확인
## git checkout main 메인 포인터로 돌아오기
## git revert [고유ID] 과거 버전으로 되돌리기

브랜치
## git branch 브랜치 조회
## git branch -d 브랜치 삭제
## git branch [브랜치명] 브랜치 생성
## git checkout [브랜치명] 브랜치 이동
## git merge 브랜치 합치기
## git stash 임시저장
## git diff 변경사항 비교
## git switch -c [새브랜치명] [커밋ID]
## 



# git checkout

git은 .git/refs/heads/[브랜치명] 을 포인터로 지정하고 작업한다.
브랜치에 따라 objects에 파일을 꺼낸다.  
checkout은 헤더 포인터를 바꾸는것.

checkout [고유ID] 헤더를 바꾸지않고 메인헤더의 과거를 보는것
브랜치에서 과거 버전을 보기위해선 포인터 헤더를 바꾸면됨




# git 브랜치

branch 나뭇가지
main의 해시값을 그대로 가져가면서 포인터를 붙여 구분하는것
메모장 여러개 켜 놓는 것과 동일함

git clone -> git branch [브랜치명] -> git checkout [브랜치명] -> 작업 -> git checkout main -> git merge [브랜치명]


git/refs/heads/main -> 기본 브랜치 파일
git branch [브랜치명1] ->  .git/refs/heads/[브랜치명1]
git branch [브랜치명2] ->  .git/refs/heads/[브랜치명2]



# git 커밋 태그

feat - 새 기능 추가
fix - 버그 수정
docs - 문서 수정
stlye - 코드 자체 로직 변경 없음
refactor - 코드 구조 개선
test - 테스트 코드
chore - 인프라 환경 설정 수정, 빌드, 패키지 매니저 설정
