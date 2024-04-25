# Vim

```shell
$ yum -y install vim-enhanced   # 기능이 많은 버전설치
$ vi /etc/profile
alias vi = "vim"
```

-   문자 코드 지정
    -   set encoding=utf-8
-   파일 코딩 지정
    -   set fileencoding=utf-8
-   개행 코드 지정
    -   set fileformats=unix,dos
-   백업 설정 활성화
    -   set backup
-   백업 설정 비활성화
    -   set nobackup
-   백업파일 생성하는 디렉토리 지정
    -   set backupdir=~/backup
-   검색 이력 개수 설정
    -   set history=50
-   검색시 대소문자 구별 하지 않고 검색하게 설정
    -   set ignorecase
-   검색시 대소문자를 같이 써서 검색하면 대소문자를 구별해서 검색하도록 설정
    -   set smartcase
-   검색시 일치하는 단어 하이라이트 표시하기
    -   set hlsearch
-   검색시 일치하는 단어 하이라이트 표시하지 않기
    -   set nohlsearch
-   검색시 검색어를 입력하는 도중에도 검색을 시작하는 설정
    -   set incsearch
-   검색시 검색이 입력이 완료해야 검색하는 설정
    -   set noincsearch
-   행번호를 표시하는 설정
    -   set number
-   행번호를 표시하지 않는 설정
    -   set nonumber
-   줄바꿈시 ($)표시나 (^|)를 표시하는 설정
    -   set list
-   괄호를 사용시 열고 닫히는 관계의 괄호를 강조하는 설정
    -   set showmatch
-   파일의 끝에 있는 개행을 자동으로 제거하는 설정
    -   set binary noeol
-   자동 인덴트 활성화 설정
    -   set autoindent
-   자동 인덴트 비활성화 설정
    -   set noautoindent
-   문법에 맞게 색상 표시하는 기능 설정
    -   syntax on
-   문법에 맞게 색상 표시 기능 비활성화 설정
    -   syntax off
-   syntax on 했을 때 주석의 색을 변경
    -   highlight Comment ctermfg=LightCyan
-   윈도우 넓이와 높이를 접을 수 있게하는 설정
    -   set wrap
-   윈도우 넓이와 높이를 접을 수 없게하는 설정
    -   set nowrap

" Syntax Highlighting
if has("syntax")
syntax on
endif
set hlsearch " 검색어 하이라이팅
set nu " 줄번
set autoindent " 자동 들여쓰기
set ts=4 " tag select
set sts=4 " st select
set cindent " C언어 자동 들여쓰기
set laststatus=2 " 상태바 표시 항상
set shiftwidth=4 " 자동 들여쓰기 너비 설정
set showmatch " 일치하는 괄호 하이라이팅
set smartcase " 검색시 대소문자 구별
set smarttab
set smartindent
set ruler " 오른편 하단에 현재 커서 위치 표시
set fileencodings=utf8,euc-kr
set cul " 커서가 있는 라인을 하이라이트 표시
