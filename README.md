## [과거 버전으로 돌아가기]
> 아래 명령은 버전 id로 돌아가는 명령입니다. ; 공유하기 전에 자신에 작업 컴퓨터에서만 사용한다.
즉, 타임머신을 타고 시간을 되돌렸다고 생각하면 된다.
>> git reset --hard "버전 id" 
버전 id의 커밋을 취소하면서 그 내용을 새로운 버전으로 만드는 명령; push한 경우 사용한다.
즉, 취소한 사건의 이력이 추가되었다고 생각하면 됨
>> git revert "버전 id“

## [branch 만들기]
> add 하지 않고 커밋할 수 있지만, 그전에 add가 된 파일이어야 한다.
>> git commit –a –m / git commit -am
브랜치의 목록을 볼 때
>> git branch
브랜치를 생성할 때 
>> git branch "새로운 브랜치 이름"
브랜치를 삭제할 때
>> git branch -d
병합하지 않은 브랜치를 강제 삭제할 때 
>> git branch -D
브랜치를 전환(체크아웃)할 때
>> git checkout "전환하려는 브랜치 이름"
브랜치를 생성하고 전환까지 할 때 
>> git checkout -b "생성하고 전환할 브랜치 이름“

## [branch 정보확인]
> 브랜치 간에 비교할 때, 브랜치1에는 없고 브랜치2에만 있는 것을 비교해서 보여줌
>> git log "비교할 브랜치 명 1".."비교할 브랜치 명 2“
브랜치1에는 없고 브랜치2에만 있는 것을 비교해서 보여줌, 그리고 소스코드를 비교함
>> git log –p "비교할 브랜치 명 1".."비교할 브랜치 명 2“
브랜치 간의 코드를 비교 할 때, 각각의 브랜치의 현재 상태 비교할 때 
>> git diff "비교할 브랜치 명 1".."비교할 브랜치 명 2"
로그에 모든 브랜치를 표시하고, 그래프로 표현하고, 브랜치 명을 표시하고, 한줄로 표시할 때 
>> git log --branches --graph --decorate --oneline

## [branch 병합]
> A 브랜치로 B 브랜치를 병합할 때 (A ← B)
>> git checkout A
>> git merge B

## [원격 저장소 만들기(Github)]
> $ brew install git
$ git config --global user.name "username"
$ git config --global user.email "github email address"
$ git config --list

현재 우리의 로컬저장소에 원격저장소remote repository(아래주소)를 연결시킨다. 아래주소는 origin이라는 별명을 붙여준다. origin은 기본적인 원격저장소이다.
>> git remote add origin https://github.com/DaewonMan/gitfth.git
원격 저장소의 상세보기
>> git remote –v
원격저장소로 나의 작업을 보낼 때 로컬저장소 입장에서 원격저장소로 푸쉬
현재 checkout되어 있는 로컬저장소의 branch를 origin에 해당하는 저장소를 master로 동기화시킨다.
>> git push -u origin master
새로운 버전을 만들었을 때 간단하게 동기화할 수 있다.
>> git push
새로운 디렉토리를 만들고 그 디렉토리를 로컬저장소로 만들 때
>> mkdir gitfth2
>> cd gitfth2
>> git clone https://github.com/DaewonMan/gitfth.git . (현재디렉토리(.)에 복제한다)

## [원격저장소와 지역저장소의 동기화 방법(Github)]
> 여러대의 컴퓨터를 진행할 때 프로젝트를 수월하게 진행할 수 있다.

커밋한 버전의 이름을 수정한다.
>> git commit —amend
원격저장소에 있는 내용을 지역저장소로 끌어온다. 어떠한 작업을 하기 전에 이 명령어 사용
>> git pull

## [로그인 없이 원격저장소 이용하기(Github)]
> ssh = Secure Shell
공개키와 비밀키를 이용해서 깃허브 로그인 없이 파일을 업로드할 수 있다.

공개키와 비밀키를 생성한다.
>> ssh-keygen
홈디렉토리를 ~로써 지정할 수 있다. .ssh디렉토리에 공개키와 암호키가 있다.
>> ~/.ssh
id_rsa는 private key이고 id_rsa.pub는 public key이다. 
cat id_rsa.pub을 통해서 공개키를 알아내고 그것을 복사해서 깃허브 계정에 등록을 한다. 설정->ssh
>> git clone git@github.com:DaewonMan/gitfth_ssh.git [디렉토리명 gitfth_ssh]
>> vim f1.txt
>> git add f1.txt
>> git commit –m 1
>> git push

## [원격저장소의 원리]
> [pull과 fetch의 차이점]
일반적으로 pull을 사용하지만 정교한 작업이 필요할 땐 fetch
git pull을 하면 지역저장소인 refs/heads/master와 원격저장소인 logs/refs/remotes/origin/master가 가리키는 버전은 같다.
git fetch를 하면 지역저장소인 refs/heads/master은 이전의 버전을 가르키고 원격저장소인 logs/refs/remotes/origin/master는 최근의 push한 버전을 가르킨다.
즉, 원격저장소에는 최근 커밋을 저장해놨지만 지역저장소에는 어떠한 변화도 가하지 않는다.
따라서 원격저장소의 있는 내용과 지역저장소의 차이점을 비교해볼 수 있다.
코드를 비교하고 싶으면 >> git diff HEAD origin/master
문제가 없다면 >> git merge origin/master을 통해서 병합한다. 그러면 지역, 원격저장소가 같은 커밋을 가르킨다.

## [태그(tag)]
> git에서 tag는 특정한 커밋 버전을 설명한다.

태그 목록 보기
>> git tag
태그 생성 (light weight tag)
>> git tag "태그 이름" [태그가 가르킬 버전의 커밋 아이디]
태그 생성 (annotated tag)
>> git tag -a "태그 이름" -m "태그에 대한 설명" [태그가 가르킬 버전의 커밋 아이디]
태그 삭제
>> git tag -d "삭제할 태그명"
로컬에서 만든 태그를 원격 저장소로 업로드
>> git push —tags

## [Rebase]
> rebase VS merge
똑같은 병합하는 방법이지만 결과가 다르다.
git rebase “병합하고자하는 브랜치”를 하면 병합하고자하는 브랜치의 최신 버전을 base로 두고 현재 checkout된 브랜치의 버전들이 base의 상위에(최신에) 올라가게 된다.

rebase는 다른 사람과 공유하지 않은 커밋들에 대해 rebase해야한다.

"강의 보았습니다만, 개인적으로는 merge보다 rebase를 선호하고, 오히려 rebase를 안전하게 느끼고 있습니다. 중간에 conflict를 수정하다 어려움을 만나도 언제든지 rebase --abort로 rebase 작업을 취소할 수 있고, 심지어 그것 조차도 부담이 된다면, rebase 전에 임시 branch를 백업 용도로 만들었다가 rebase 후에 삭제하는 방법을 사용하기도 합니다.

세번째 강의에서처럼 지속적으로 conflict가 발생하는 경우라면, 아예 master에 임시 branch를 만들고 커밋별로 cherry-pick을 하기도 합니다.
rebase와 cherry-pick으로 히스토리를 정리한 뒤 push하면 master 브랜치 관리자가 해당 branch를 확인후 fast-forward 방식만으로 master를 관리하기 쉽게 만들어준다는 장점이 있습니다." (안신열님의 의견)