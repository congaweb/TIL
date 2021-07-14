# Start git

## git 사용 전 필요한 내용

### MacOS

1. iTerms
2. Xcode Command Line Tools(`$ xcode-select --install`)
3. ohMyZsh
4. Homebrew


### Windows

- [git for windows](https://gitforwindows.org) (git bash 실행하여 사용)


### Shell Command

#### 디렉토리 생성 및 이동

`$ cd Documents` : 디렉토리 들어가기

`$ mkdir dev` : 디렉토리 만들기

`$ cd ..` : 상위 디렉토리 들어가기

`$ pwd` : 현재 디렉토리 보기

`$ ls` : 폴더나 파일의 리스트 보여주기 (`-l`, `-a`, `-al` 등의 플래그가 있음)

#### 파일 생성 및 이동, 삭제

`$ touch readme.md` : 파일 생성

`$ mv readme.md bin/` : 파일 이동

`$ cp readme.md bin/` : 파일 복사

`$ mv readme.md ./READEME.md` : 파일명 변경

`$ rm README.txt` : 파일 삭제 (폴더 삭제 시 `-rf` 플래그 사용. 단, 오브젝트까지 모두 삭제하는 플래그이므로 조심해서 사용 할 것.)

#### 파일 열기 및 수정, 내용 확인

`$ vi readme.md` : vim 에디터를 통해 파일 작성 및 수정

`$ cat readme.md` : 파일 내용 확인 

#### 기타

`sudo` : 관리자 권한으로 실행

#### Vim command

vim 에디터로 파일 열 경우, 처음은 normal 모드.

입력을 위해서는 `i`로 insert 모드로 변경, `:`로 command 모드

`esc`버튼으로 normal 모드로 돌아올 수 있음.

하기 명령어는 vim에서 쓰이는 명령어

##### normal mode

`h j k l` :  left, down, up, right

`i` : insert mode

`v` : visual mode

`ESC` : back to normal mode

`d` : delete

`dd` : delete a line

`Y` : yank

`p` : paste

`u` : undo

`a` : append

##### Command mode

`:q` : quit

`:q!` : quit discarding all changes (변경사항 저장하지 않고 종료)

`:w` : write (저장)

`:wq` : write and quit (저장 및 종료)

`:{number}` : jump to {number}th line


## git이란

Linus Torvalds가 만든 버전 관리 시스템.

빠른 속도, 단순한 구조, 분산형 저장소 지원, 비선형적 개발(수천개의 브랜치) 가능하다는 장점이 있음.

소스코드 주고 받기 없이 동시 작업 가능. 수정은 commit 단위로 관리, 배포 뿐 아니라 원하는 시점으로 Checkout 가능.
새로운 기능 추가는 **branch**로 개발, 개발 완료 시 **merge**하여 반영

GUI 툴을 사용하기에 앞서 CLI로 작업하는 방법을 익히는 것이 좋다.

*한문장으로 정리한 git flow => 작업한 뒤 메모해서(local) 넘긴다(remote)*

### git objects

- blob : 파일 하나의 내용에 대한 정보

- Tree : Blob이나 subtree의 메타디에터 (디렉토리 위치, 속성, 이름 등)

- Commit : 커밋 순간의 스냅샷

## git 시작하는 법

### git 설치 및 환경설정

- git 설치 확인 (`$ git --version`)
- git 환경 설정

```shell
$ git config --global user.name "{github username}"
$ git config --global user.email "{github email address}"
$ git config --global core.editor "vim"
$ git config --global core.pager "cat"
$ git config --list
```

- optional
`$ git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"`

- `$ git config --list`로 정상 설정 확인 가능
- 잘못 설정했을 경우 입력값을 다시 넣거나, `$ git config --global --unset {key}`로 삭제 가능

### git으로 project 시작하는 첫번째 방법: git init
작업공간에서 시작하여 github으로 소스코드를 내보냄.

1.프로젝트 폴더 만들기

```shell script
$ mkdir practice-git
$ cd practice-git
```
2.init 명령으로 local repository로서 역할을 시작
```shell script
$ git init
```
*만약 초기 branch 네임이 master로 셋팅 될 경우 `$ git branch -M main` 명령어를 통해 브랜치 네임을 main으로 변경할 것.*

3.github에서 새롭게 비어있는 remote repository를 생성하고, 복사한 주소를 local repository에 등록.

*remote respository 이름은 컴퓨터에서 생성한 새 폴더와 이름을 맞춰 차후 헷갈리자 않도록 할 것*
```shell script
$ git remote add origin 복사한주소
```
*여기서 origin은 복사한 주소를 부르기 위한 이름으로, 다른이름을 사용 가능*

- 추가되었는지 확인하는 명령어
```shell script
$ git remote get-url origin
```

4.새파일을 만들고 작업을 수행 (파일의 수정은 에디터에서 진행해도 됨.)
```shell script
$ touch README.md
$ vi README.md
```

5.작업이 끝났다면 `$ git status` 명령으로 현재 프로젝트의 상태 확인

`untracked files: README.md`가 보인다면 다음 작업을 할 준비가 됨.

6.workspace에 추가된 새로운 파일을 index로 staging

`$ git add READEME.md`

7.추가된 README.md에 대한 설명을 commit

`$git commit`

`core.editor=vim`으로 설정했기 때문에 vim 에디터로 commit 메시지 작성 가능

첫 줄에 들어가는 내용이 제목, 세번째 줄부터 들어가는 내용이 상세 설명이 됨.

모든 작업이 끝났다면 `$ git status`를 입력해 commit 할 내역이 있는지 확인.

*`$ git commit -m "커밋메시지"`를 입력하면 커맨드라인에서 바로 commit message 입력 가능*

8.commit이 끝났다면 remote repository로 push

**첫 commit이라면** -u(-set-upstream) flag를 붙여 push하여 현재 작업중인 branch가 업로드할 branch의 변동사항을 추적하도록 설정.
`$ git push -u origin main`

이후에는 -u 옵션 없이 바로 push
`$ git push origin main`

9.4~8의 작업을 반복 수행.

### git으로 project 시작하는 두번째 방법 : git clone

github에서 remote repository를 먼저 생성한 뒤, 작업공간으로 끌어와 작업을 시작.

1.github에서 remote repository를 생성하되, LICENSE, README.md, .gitignore 등의 파일과 함께 생성. Clone or Download 버튼을 눌러 해당 repository의 주소를 복사.

2.Terminal에서 `$ git clone 복사한주소`를 입력하여 작업공간에 local repository를 생성.

3.새 파일을 만들고 작업을 수행 (파일의 수정은 에디터에서 진행해도 됨.)
```shell script
$ touch README.md
$ vi README.md
```

4.작업이 끝났다면 `$ git status` 명령으로 현재 프로젝트의 상태 확인

`untracked files: README.md`가 보인다면 다음 작업을 할 준비가 됨.

5.workspace에 추가된 새로운 파일을 index로 staging

`$ git add READEME.md`

6.추가된 README.md에 대한 설명을 commit

`$git commit`

7.commit이 끝났다면 remote repository로 push

remote repository에서 먼저 끌어와 사용하는 구조이기 때문에 remote repository의 master 브랜치와 local repository의 master 브랜치는 추적하도록 세팅되어 있음.

따라서, 위의 -u flag를 붙이지 않아도 됨.

`$ git push origin main`

8.3~7의 작업을 반복 수행

## Markdown
markdown 문법은 하기 내용 참고하여 사용.
[markdown 문법 정리](https://heropy.blog/2017/09/30/markdown/)

## Done

1. TIL 작성하기

## TODO

1. css 온라인 강의 시청 및 html 복습
2. gitblog 복습 및 TIL 작성