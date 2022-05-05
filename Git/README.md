# Git

## Git을 공부해야 되는 이유
Git은 코드 관리와 다른 개발자와의 협업에 도움을 주며 개발 실력을 향상시켜준다. 따라서 Git을 공부해야 된다.

## 버전 관리 시스템
버전 관리 시스템(VCS - Version Control System)은 파일 변화를 시간에 따라 기록했다가 나중에 특정 시점의 버전을 다시 꺼내올 수 있는 시스템이다. 따라서 VCS를 사용하여 파일을 이전 상태로 돌리거나 누가 문제를 일으켰는지 추적할 수 있고 파일을 잃어버렸을 때 쉽게 복구할 수 있다.

### 로컬 버전 관리
![로컬 버전 관리](https://git-scm.com/book/en/v2/images/local.png)  
로컬 버전 관리 시스템은 파일에서 변경되는 부분(Patch Set)을 저장한 후 일련의 Patch Set을 적용하여 파일을 특정 시점으로 되돌릴 수 있다.

### 중앙집중식 버전 관리
![중앙집중식 버전 관리](https://git-scm.com/book/en/v2/images/centralized.png)  
중앙집중식 버전 관리 시스템은 파일을 관리하는 중앙 서버가 별도로 있고 클라이언트가 중앙 서버에서 파일을 받아서 사용한다. 중앙집중식 버전 관리 시스템의 결점은 중앙 서버에 문제가 발생하였을 때 협업이 불가능하며 중앙 데이터베이스가 있는 하드디스크에 문제가 발생했을 경우 프로젝트의 모든 히스토리를 잃게 된다는 점이다.

### 분산 버전 관리
![분산 버전 관리](https://git-scm.com/book/en/v2/images/distributed.png)  
분산 버전 관리 시스템에서 클라이언트는 저장소를 히스토리와 더불어 전부 복제하며 서버에 문제가 발생한 경우 복제물로 다시 작업을 한다. Git은 분산 버전 관리 시스템이다.

## Git의 개념 및 동작
* Git은 데이터를 파일 시스템 스냅샷의 스트림으로 취급하며 크기가 작다.
* Git은 커밋을 하거나 프로젝트의 상태를 저장할 때마다 파일이 존재하는 순간을 중요하게 생각하며 파일이 수정되지 않았으면 파일을 새로 저장하지 않고 이전 상태의 파일에 대한 링크만 저장한다.
* Git의 거의 모든 명령은 로컬 파일과 데이터만 사용한다. 따라서 오프라인 상태에서도 작업이 가능하다.
* Git은 데이터를 저장하기 전에 체크섬을 구하여 데이터를 관리한다. 따라서 Git 없이는 체크섬을 다룰 수 없기 때문에 파일 혹은 디렉토리의 변경이 불가능하다.
* Git은 파일을 Committed, Modified, Staged의 세가지 상태로 관리한다.
  * Committed는 데이터가 로컬 데이터베이스에 안전하게 저장되었다는 것을 의미한다.
  * Modified는 수정한 파일을 아직 데이터베이스에 커밋하지 않은 것을 말한다.
  * Staged는 현재 수정한 파일을 곧 커밋할 것이라고 표시한 상태를 의미한다.
* 위의 세가지 상태는 Git 프로젝트의 세 가지 단계(Working Tree, Staging Area, Git Directory)와 연결되어 있다.
  * Working Tree는 프로젝트의 특정 버전을 Checkout 한 것을 말한다. Git Directory는 작업하는 디스크에 있으며 압축된 데이터베이스에서 파일을 가져와 Working Tree를 만든다.
  * Staging Area는 Git Directory에 있으며 커밋할 파일에 대한 정보를 저장한다. Git에서는 기술용어로 index라고 한다. 
  * Git Directory는 Git이 프로젝트의 메타데이터와 객체 데이터베이스를 저장하는 곳이다. 다른 컴퓨터에 있는 저장소를 Clone 할 때 만들어지는 것이 Git Directory이다.  

![Git 프로젝트 단계](https://git-scm.com/book/en/v2/images/areas.png)
* Git의 기본 워크플로우(workflow)는 다음과 같다.
    1. Working Tree에서 파일을 수정한다.
    2. Staging Area에 파일을 Stage하여 커밋할 스냅샷을 만든다.
    3. Staging Area에 있는 파일들을 커밋하여 Git Directory에 스냅샷으로 저장한다.
* Git Directory에 있는 파일들은 Committed된 상태이다. 파일을 수정한 뒤 Staging Area에 추가하면 Staged이다. 그리고 Checkout 하고 난 뒤 파일을 수정하였지만 아직 Staging Area에 추가하지 않았다면 Modified이다.

## Git 설치
Git을 설치하기 위해서는 먼저 Homebrew를 설치해야 된다.  
Homebrew를 설치하는 방법은 brew.sh 사이트에서 확인할 수 있으며 나는 macOS를 사용하므로 다음 코드를 터미널에 입력하여 설치하였다.
```zsh
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
Homebrew 설치가 완료되면 다음 코드를 터미널에 입력하여 Git을 설치한다.
```zsh
$ brew install git
```

## Git 설정 (macOS)
Git을 설치했으면 Git의 사용 환경을 설정해주어야 한다. 모든 사용 환경이 gitconfig 파일에 저장되며 다음 코드를 터미널에 입력하면 이를 확인할 수 있다.
```zsh
$ git config --list # Terminal
```
```zsh
$ git config --global -e # Editor
```
다음으로 gitconfig에 이름과 이메일을 설정한다.
```zsh
$ git config --global user.name "yuminyumin"
$ git config --global user.email "jungym887@naver.com"
```
다음으로 OS마다 캐리지 리턴(carriage-return)이 다른 것을 보완해주기 위해 다음 코드를 터미널에 입력한다.
```zsh
$ git config --global core.autocrlf input
```

## Git 초기화 및 삭제
Git을 초기화 하기 위해서는 터미널에서 해당 프로젝트의 디렉토리로 들어가 다음 코드를 순서대로 입력하면 된다.
```zsh
$ cd projects
$ mkdir git
$ git init
```
이렇게 Git을 초기화하면 master branch가 생성된다. 여기서 다시 Git을 삭제하려면 다음 코드를 입력한다.
```zsh
$ rm -rf .git
```

## Git의 기초

### Git 저장소 만들기
Git 저장소를 사용하는 방법에는 두 가지가 있다.
1. 버전 관리를 하지 않는 기존 디렉토리를 Git 저장소로 사용하는 방법
2. 어딘가에서 Git 저장소를 Clone 하는 방법
   
### 기존 디렉토리를 Git 저장소로 사용하는 경우
이 경우에는 우선 프로젝트의 디렉토리로 이동한다. 그리고 다음 명령을 터미널에 입력한다.
```zsh
$ git init
```
이 명령은 `.git`이라는 하위 디렉토리를 만든다. `.git`디렉토리에는 저장소에 필요한 스켈레톤 파일이 들어있다.
Git이 파일을 관리하게 하기 위해서는 저장소에 파일을 추가하고 커밋해야 한다.
```zsh
$ git add *.c # File
$ git commit -m 'initial project version'
```
### 기존 저장소를 Clone하여 사용하는 경우
다른 프로젝트에 참여하거나 Git 저장소를 복사하고 싶을 때는 `git clone <url>` 명령을 사용한다.  
예를 들어 libgit2 라이브러리 소스코드를 Clone 하기 위해서는 아래와 같은 명령을 입력한다.
```zsh
$ git clone https://github.com/libgit2/libgit2
```
이 명령은 `libgit2`라는 디렉토리를 만들고 그 안에 `.git` 디렉토리를 만든다. 그리고 저장소의 데이터를 모두 가져와 최신 버전을 Checkout 해 놓으며 당장 하고자 하는 작업을 시작할 수 있다.  
저장소를 Clone할때 다른 이름을 사용하고자 하면 다음과 같이 입력하면 된다. 예시에서는 `mylibgit`이라는 이름으로 디렉토리를 만들었다.
```zsh
$ git clone https://github.com/libgit2/libgit2 mylibgit
```

### 파일을 수정하고 저장소에 저장하기
파일을 수정하고 파일의 스냅샷을 커밋하여 저장소에 저장해보자.  
워킹 디렉토리의 모든 파일은 `Tracked`와 `Untracked`로 나누며 `Tracked`파일은 이미 스냅샷에 포함되어 있던 파일이다. `Tracked` 파일은 다시 `Unmodified`와 `Modified` 또는 `Staged` 상태 중 하나이며 Git이 알고 있는 파일이다.  
그리고 나머지 파일은 모두 `Untracked` 파일이며 `Untracked` 파일은 워킹 디렉토리에 있는 파일 중 스냅샷에도 `Staging Area`에도 포함되지 않은 파일이다.  
마지막 커밋 이후에 어떤 파일을 수정하면 Git은 그 파일을 `Modified` 상태로 인식하며 커밋을 하기 위해서는 수정한 파일을 `Staged` 상태로 만들어 커밋을 하게 된다. 따라서 파일의 라이프 사이클(lifecycle)은 다음과 같다.  
![파일의 라이프사이클](https://git-scm.com/book/en/v2/images/lifecycle.png)

### 파일의 상태 확인하기
파일의 상태를 확인하기 위해서는 `git status` 명령을 사용한다.  
프로젝트에 README 파일을 만들고 `git status` 명령을 사용해보자.
```zsh
$ 'My Project' > README
$ git status
```
`git status` 를 확인해보면 README파일은 `Untracked` 상태라는 것을 알 수 있다. Git에서 `Untracked` 상태는 아직 스냅샷에 넣어지지 않은 파일이라고 생각하며 파일이 `Tracked` 상태가 되기 전까지는 커밋을 하지 않는다. 그렇다면 README 파일을 `Tracked` 상태로 만들어보자.

### 파일을 트래킹(Tracking) 하기
`git add` 명령으로 파일을 새로 트래킹할 수 있다. Git이 README 파일을 트래킹하도록 해보자.
```zsh
$ git add README
```
이 때 `git status` 명령을 실행하면 README 파일이 `Tracked` 상태이면서 `Staged` 상태임을 확인할 수 있다. `git add` 명령은 파일 또는 디렉토리를 매개변수로 받으며 디렉토리의 경우 아래의 파일들까지 재귀적으로 추가한다.

### Modified 상태의 파일을 Stage 하기
`CONTRIBUTING.md` 라는 파일을 수정하고 나서 `git status` 명령을 다시 실행하면 `CONTRIBUTING.md` 파일은 Changes not staged for commit 에 있는 것을 확인할 수 있다. 이는 `Tracked` 상태이지만 아직 `Staged` 상태는 아니라는 것이다. 이를 `Staged` 상태로 만들기 위해서는 `git add` 명령을 실행해야 한다. 
```zsh
$ git add CONTRIBUTING.md
```
다시 `git status` 명령을 실행하면 `CONTRIBUTING.md` 파일이 `Staged` 상태임을 확인할 수 있다. 하지만 이때 `CONTRIBUTING.md` 파일을 열고 수정한 다음 다시 `git status` 명령을 실행하면 `CONTRIBUTING.md` 파일이 `Staged` 상태이면서 동시에 `Unstaged` 상태임을 알 수 있다. 이는 커밋을 할 때 커밋을 하는 시점의 버전이 커밋되는 것이 아니라 마지막으로 `git add` 명령을 실행했을 때의 버전이 커밋되기 때문에 `git add` 명령을 실행한 후에 파일을 수정했으면 `git add` 명령을 다시 실행하여 최신 버전을 `Staged` 상태로 만들어야 한다.

### 파일 상태를 간단하게 확인하기
`git status`를 사용하여 상태를 확인할 때 내용이 많아 보일 수 있다. 그래서 상태를 더욱 간단하게 확인하는 방법이 있다.
```zsh
$ git status -s
```
이때 아직 트래킹하지 않는 새 파일 앞에는 `??`, Staged 상태로 추가한 파일 중 새로 생성한 파일 앞에는 `A`, 수정한 파일 앞에는 `M` 표시가 붙는다. 이 명령의 결과에서 상태정보 칼럼에는 왼쪽에는 `Staging Area`에서의 상태를 오른쪽에는 `Working Tree`에서의 상태를 표시한다. 

### 파일 무시하기
보통 로그 파일이나 빌드 시스템이 자동으로 생성한 파일은 Git이 관리할 필요가 없다. 이런 파일들을 무시하기 위해서는 `.gitignore` 파일을 만들고 그 안에 무시할 파일의 패턴을 만든다. `.gitignore` 파일은 보통 처음에 만들어 두는 것이 편리하며 Git 저장소에 커밋하고 싶지 않은 파일을 커밋하는 실수를 방지한다.  
`.gitignore` 파일에 입력하는 패턴은 다음 규칙을 따른다.
* 아무것도 없는 라인이나 `#`로 시작하는 라인은 무시한다.
* 표준 글로브 패턴을 사용한다.
* `/`로 시작하면 하위 디렉토리에 적용되지 않는다.
* 디렉토리는 끝에 `/`를 사용하여 표현한다.
* `!`로 시작하는 패턴의 파일은 무시하지 않는다.
`.gitignore` 파일의 예시는 [github/gitignore](https://github.com/github/gitignore)에서 확인이 가능하다.

### Staged와 Unstaged 상태의 변경 내용 보기
파일이 변경됐다는 사실이 아니라 어떤 내용이 변경되었는지를 확인하기 위해서는 `git diff` 명령을 사용한다. `git diff` 명령을 실행하면 아직 `Staged` 상태가 아닌 파일을 비교해 볼 수 있다. 이 명령은 `Working Directory`와 `Staging Area`에 있는 것을 비교한다. 만약 `Staging Area`에 넣은 파일의 변경 부분을 보고싶으면 `git diff --staged` 옵션을 사용한다.

### 변경사항 커밋하기
수정한 것을 커밋하기 위해 `Staging Area`에 파일을 정리했으면 `git commit`을 실행하여 커밋한다.
```zsh
$ git commit
```
메시지를 인라인으로 첨부하고자 하는 경우에는 다음과 같이 명령하면 된다.
```zsh
$ git commit -m "message"
```

### Staging Area 생략하기
`Staging Area`는 커밋할 파일을 정리한다는 점에서 매우 유용하지만 복잡하여 필요하지 않은 때도 있다. 이때는 `git commit` 명령을 실행할때 `-a` 옵션을 추가하면 Git은 `Tracked` 상태의 파일을 바로 `Staging Area`에 넣어 `git add` 명령을 실행하는 수고를 덜어준다. 

### 파일 삭제하기
Git에서 파일을 제거하려면 `git rm` 명령으로 파일을 `Staging Area`에서 삭제한 후에 커밋해야 한다. 이 명령은 실제 `Working Directory`에 있는 파일도 삭제하기 때문에 실제 파일도 지워진다. 

### 파일 이름 변경하기
다음 명령을 입력하여 파일의 이름을 변경할 수 있다.
```zsh
$ git mv file_from file_to
```

### 커밋 히스토리 조회하기
Git에서는 `git log` 명령을 입력하여 커밋 히스토리를 조회할 수 있다. `git log` 명령을 실행하면 커밋의 히스토리를 시간 순으로 확인할 수 있으며 커밋의 SHA-1 체크섬, 저자 이름, 저자 이메일, 커밋한 날짜, 커밋 메시지를 보여준다. `git log` 명령에는 다양한 옵션이 있다. `-p` 또는 `--patch` 옵션은 각 커밋의 `diff` 결과를 보여주며 `$ git log -p -2`와 같이 사용하는 경우 최근 두 개의 결과를 보여준다. `--stat` 옵션은 각 커밋의 통계 정보를 조회해주며 어떤 파일이 수정되었는지, 얼마나 많은 파일이 변경되었는지, 얼마나 많은 라인을 추가하거나 삭제했는지 보여준다. `--pretty` 옵션은 히스토리를 조회할 때 다양한 형식으로 볼 수 있게 지원해준다. `--pretty` 옵션에는 `oneline`, `short`, `full`, `fuller` 등의 옵션이 있으며 이 중 `format` 옵션은 나만의 포맷으로 결과를 출력하고자 할 때 사용한다. 다음과 같이 입력하여 사용한다.
```zsh
$ git log --pretty=format:"%h - %an, %ar : %s"
```
`format` 옵션에서 사용할 수 있는 옵션은 [pretty_format](https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-%EC%BB%A4%EB%B0%8B-%ED%9E%88%EC%8A%A4%ED%86%A0%EB%A6%AC-%EC%A1%B0%ED%9A%8C%ED%95%98%EA%B8%B0#pretty_format)에서 확인할 수 있다.
`oneline` 옵션과 `format` 옵션은 `--graph` 옵션과 함께 사용할 수 있으며 `--graph` 명령은 브랜치와 머지 히스토리를 보여주는 아스키 그래프를 출력한다.  

### 조회 제한조건
`git log` 명령은 `--since`, `--until` 같은 시간을 기준으로 조회하는 옵션을 사용할 수 있다. 지난 2주동안 만들어진 커밋을 조회하는 명령은 다음과 같다.
```zsh
$ git log --since=2.weeks
```
`--author` 옵션으로 저자를 지정하여 검색할 수도 있으며 `--grep` 옵션으로 커밋 메시지에서 키워드를 검색할 수도 있다. `-S` 옵션은 코드에서 추가되거나 제거된 내용중에 특정 텍스트가 있는지를 검색한다.

### 되돌리기
완료한 커밋을 수정하고 싶을 때는 파일 수정 작업을 하고 난 후에 `Staging Area`에 추가한 다음 `--amend` 옵션을 사용하여 커밋을 재작성한다.
```zsh
$ git commit --amend
```
커밋을 했는데 Stage하는 것을 빠트린 파일이 있다면 다음과 같은 명령을 입력하면 된다.
```zsh
$ git commit -m 'initial commit'
$ git add forgotton_file
$ git commit --amend 
```

### 파일 상태를 Unstage로 변경하기
파일 두 개를 수정하고나서 따로따로 커밋하려고 했지만 `git add *`으로 한번에 커밋해버린 경우에는 `git restore` 명령으로 파일을 `Unstaged` 상태로 변경할 수 있다. 예를 들어 `CONTRIBUTING.md` 파일을 `Unstaged` 상태로 변경하고자 하는 경우 다음과 같이 명령을 입력하면 된다.
```zsh
$ git restore --staged CONTRIBUTING.md
```

### Modified 파일 되돌리기
`CONTRIBUTING.md` 파일을 수정하고 나서 최근에 커밋된 버전으로 되돌리고자 할 때는 다음 명령을 입력하면 된다.
```zsh
$ git restore CONTRIBUTING.md
```

### 리모트 저장소
리모트 저장소는 인터넷 혹은 네트워크 어딘가에 있는 저장소(로컬에 있는 경우도 있음)를 말한다. 리모트 저장소를 관리할 줄 알아야 다른 사람들과 협업할 수 있다.

### 리모트 저장소 확인하기
`git remote` 명령으로 현재 프로젝트에 등록된 리모트 저장소를 확인할 수 있다. 이 명령은 리모트 저장소의 단축 이름을 보여주며 저장소를 clone한 경우에는 자동으로 `origin`이라는 리모트 저장소가 등록되기 때문에 `origin`이라는 이름을 볼 수 있다. 이 때 `-v` 옵션을 주면 단축이름과 URL을 함께 볼 수 있다. 만약 리모트 저장소가 여러 개 있다면 이 명령은 등록된 정보를 모두 보여준다. 

### 리모트 저장소 추가하기
기존 `Working Directory`에 새 리모트 저장소를 추가할 수 있는데 `git remote add <shortname> <url>` 명령을 사용한다. 예를 들어 다음과 같은 명령을 입력하면 URL 대신 `pb`라는 이름을 사용할 수 있다.
```zsh
$ git remote add pb https://github.com/paulboone/ticgit
```

### 리모트 저장소를 Pull 하거나 Fetch하기
리모트 저장소에서 데이터를 가져오기 위해서는 다음과 같이 명령을 입력하면 된다.
```zsh
$ git fetch <remote>
```
이 명령은 로컬에는 없지만 리모트 저장소에는 있는 데이터를 모두 가져온다. 그러면 리모트 저장소의 모든 브랜치를 로컬에서 접근할 수 있어 언제든 Merge하거나 내용을 살펴볼 수 있다. 저장소를 Clone하면 자동으로 리모트 저장소를 `origin`이라는 이름으로 추가한다. 그래서 나중에 `git fetch origin`이라는 명령을 입력하면 Clone 한 이후에 수정된 내용들을 모두 로컬로 가져오지만 자동으로 `Merge` 하지는 않는다. 그러므로 로컬에서 작업을 완료한 후에 수동으로 `Merge`를 해야 한다. `git pull` 명령으로는 리모트 저장소 브랜치에서 데이터를 가져올 뿐 아니라 자동으로 로컬 브랜치와 Merge시킬 수 있다.

### 리모트 저장소에 Push하기
프로젝트를 공유하고 싶을 때는 `git push <remote> <branch>` 명령을 이용하여 서버에 Push한다. 만약 `master` 브랜치를 `origin`서버에 Push하고자 한다면 다음과 같이 명령을 입력하면 된다.
```zsh
$ git push origin master
```
이 명령은 Clone 한 리모트 저장소에 쓰기 권한이 있고 Clone 하고 난 뒤에 아무도 저장소에 Push를 하지 않았을 경우에만 사용할 수 있다. 만약 다른 사람이 먼저 Push한 것이 있을 경우에는 Merge한 후에 Push를 해야된다.

### 리모트 저장소 살펴보기
`git remote show <remote>` 명령으로 리모트 저장소의 구체적인 정보를 확인할 수 있다. 이 명령은 리모트 저장소의 URL과 트래킹하는 브랜치를 출력한다. 이 명령은 `git pull` 명령을 실행할 때 master브랜치와 Merge할 브랜치가 무엇인지 보여준다. 

### 리모트 저장소 이름을 바꾸거나 리모트 저장소를 삭제하기
`git remote rename` 명령으로 리모트 저장소의 이름을 변경할 수 있다. 예를 들어 `pb`를 `paul`로 변경하고자 한다면 다음과 같이 명령을 입력하면 된다.
```zsh
$ git remote rename pb paul
```
리모트 저장소를 삭제해야 한다면 `git remote remove` 혹은 `git remote rm` 명령을 사용한다. 보통 서버의 정보가 바뀌었을 경우 혹은 더는 기여자가 활동하지 않는 경우에 필요하다.

### 태그
Git은 태그를 지원하며 보통 릴리즈할 때 사용한다. `git tag` 명령을 입력하면 이미 만들어진 태그를 조회할 수 있다. Git의 태그는 `Lightweight` 태그와 `Annotated` 태그로 두 종류가 있다. `Lightweight` 태그는 특정 커밋에 대한 포인터이며 `Annotated` 태그는 Git 데이터베이스에 태그를 만든 사람의 이름, 이메일과 태그를 만든 날짜, 태그 메시지 등을 저장한다. 일반적으로는 `Annotated` 태그를 만들어 모든 정보를 사용할 수 있도록 하는 것이 좋다. 하지만 임시로 생성하거나 정보를 유지할 필요가 없는 경우에는 `Lightweight` 태그를 이용한다.

### Anotated 태그
`Annotated` 태그를 만드는 방법은 `tag` 명령을 실행할 때 `-a` 옵션을 추가하면 된다. 이 때 `-m` 옵션으로 태그를 저장할 때 메시지를 함께 저장할 수 있다. `git show` 명령으로 태그 정보와 커밋 정보를 모두 확인할 수 있다.

### Lightweight 태그
`Lightweight` 태그는 기본적으로 파일에 커밋 체크섬을 저장하며 다른 정보는 저장하지 않는다. `Lightweight` 태그를 만들 때는 `-a`, `-s`, `-m` 옵션을 사용하지 않고 이름만 달아준다. 

### 나중에 태그를 하는 경우
커밋을 예전에 한 경우에도 태그를 할 수 있다. 특정 커밋에 태그를 하기 위해서는 명령의 끝에 커밋 체크섬의 일부분을 명시하면 된다.
예를 들어 9fceb02로 시작하는 체크섬을 가진 커밋을 v1.2로 커밋하고자 한다면 다음과 같이 명령을 입력하면 된다.
```zsh
$ git tag -a v1.2 9fceb02
```

### 태그 공유하기
`git push` 명령은 자동으로 리모트 서버에 태그를 전송하지 않기 때문에 태그를 만들었으면 서버에 별도로 Push를 해야 한다. 이때는 `git push origin <tagname>` 을 입력하면 된다. 만약 한 번에 여러 개의 태그를 Push 하고자 하는 경우에는 `--tags` 옵션을 추가하여 `git push` 명령을 실행한다. 이 명령으로 리모트 서버에 없는 태그를 모두 전송할 수 있다.

### 태그를 Checkout 하기
태그가 특정 버전을 가리키고 있고, 특정 버전의 파일을 체크아웃해서 확인하고 싶다면 다음과 같이 실행한다. 단 브랜치를 체크아웃하는 것이 아닌 태그를 체크아웃하는 경우 `detached HEAD` 상태가 되며 일부 Git 관련 작업이 브랜치에서 작업하는 것과 다르게 동작할 수 있다. `detached HEAD` 상태에서는 작업을 하고 커밋을 만들면 태그는 그대로 있으나 새로운 커밋이 하나 쌓인 상태가 된다. 따라서 특정 태그의 상태에서 새로 작성한 커밋이 버그 픽스와 같이 의미있도록 하려면 반드시 브랜치를 만들어 작업하는 것이 좋다.

### Git Alias
Git Alias는 Git을 조금 더 쉽고 편안하게 사용할 수 있도록 만들어준다. Git의 명령을 전부 입력하는 것이 귀찮다면 `git config`를 사용하여 각 명령의 Alias를 만들 수 있다. 만약 `git commit`을 `git ci`로 간단하게 만들고자 한다면 다음과 같은 명령을 입력하면 된다.
```zsh
$ git config --global alias.ci commit
```
`!`를 제일 앞에 추가하면 실행할 수 있다. 다음과 같은 명령을 입력하면 `git visual`을 입력하면 `gitk`를 실행할 수 있다.
```zsh
$ git config --global alias.visual '!gitk'
```

## Git 브랜치
~ing

## 참고
* [Git Documentation](https://git-scm.com/doc)
* [YouTube DreamCoding](https://www.youtube.com/watch?v=Z9dvM7qgN9s&ab_channel=%EB%93%9C%EB%A6%BC%EC%BD%94%EB%94%A9by%EC%97%98%EB%A6%AC)
