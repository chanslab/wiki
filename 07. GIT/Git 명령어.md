##### 

```shell
mkdir workspace
git config --global user.name "jcsonpro"
git config --global user.email "jcson.pro@gmail.com"
# 사용자 패스워드는 안물어보는데, github에서 최근 ssh 인증을 적용해서 인듯
git hub 에서 token을 생성하고, 패스워드에 token을 입력하면 됨

```



## 도움말, 옵션 보기

```shell
$ git help config  # config 전체 도움말
$ git add -h       # add 명령어 옵션 보기
```

## global 설정
```shell
$ git config --global user.name "jcson.pro"
$ git config --global user.email jcson.pro@gmail.com
$ git config --list
$ git config -show-origin user.name # 설정을 불러오는 위치 확인
```

## 작업PC마다 branc명 변경하기
```shell
# git clone후 기본 branch 명을 office로 변경
$ git branch -m main office  # main을 office로 변경
$ git fetch origin 
$ git branch -u origin/main office  # 무슨 의미인지 모르겠음
```

## Repository clone
```shell
$ git clone https:#github.com/jcsonpro/lab.git
```
> [NOTE]   
<mark>remote: Support for password authentication was removed on August 13, 2021. Please use a personal access token instead.</mark><br>
> _Mac에서는 2021년 중반부터 password에서 token방식으로 변경_  
> * github에서 New Personal access token생성 → Mac의 keychain 삭제 → <font color="red"><u>password 대신 token을 입력하여 접속</u></font>   
토큰은 개발자 설정에서 변경가능

> "New Personal Token 생성"
> * github.com 접속
> * Setting → Development setting → Generate new token   
> * "New Personal access token" 항목 입력   
> * Note : Auth, 체크항목 모두 체크
> * "Create personal token"   
> * 생성된 token 복사   

> "Mac keychain 삭제"   
>  * command+space "keychain" 입력   
>  * "github" 검색
>  * 검색된 항목중 웹로그인 또는 login 항목 삭제


## 상태확인
```shell
$ git status
$ git diff  # branch 비교
```

## commit
```shell
$ git add -A  # 전체 파일 추가
$ git commit -m "코멘트"
$ git commit -a -m "코멘트" # 파일 추가 && commit
```

## gitignore

* 확장자가 .a인 파일 무시 <br>
```*.a```
* 확장자가 .a인 파일은 무시하게 했지만 lib.a는 무시하지 않음 <br>
```!lib.a```
* 현재 디렉토리에 있는 TODO파일은 무시하고 subdir/TODO처럼 하위디렉토리에  있는 파일은 무시하지 않음 <br>
```/TODO```
* build/ 디렉토리에 있는 모든 파일은 무시 <br>
```build/```
* doc/notes.txt 파일은 무시하고 doc/server/arch.txt 파일은 무시하지 않음 <br>
```doc/*.txt```
* doc 디렉토리 아래의 모든 .pdf 파일을 무시 <br>
```doc/**/*.pdf```


## 파일 삭제/ 파일명 변경
```shell
$ git mv README.md README
$ git rm \*~   # ~로 끝나는 파일 모두 삭제
$ git rm log/\*.txt  # log디렉토리내 txt파일 모두 삭제
```

## commit history 조회
```shell
$ git log
$ git lob -p -2 # 최근 2개의 history 비교해서 조회
```

## 리모트 저장소
```shell
$ git remote -v  # 리모트 저장소 확인
$ git remote show origin # 리모트 저장소 살펴보기
$ git remote add 리모트명 url # 리모트 저장소 추가
```
git clone을 하면 자동으로 리모트 저장소(branch) 이름은 origin이 되며,    
로컬 저장소(branch)의 이름은 master 또는 main이 된다

```shell
$ git fetch origin  # 리모트로부터 변경사항 가져오기 (No Merge)
$ git pull origin   # 리모트로부터 변경사항 가져오기 (Merge)
$ git push origin main # 로컬 저장소의 내용을 리모트로 올리기
$ git remote rename A B # 리모트 저장소 이름 변경
$ git remote rm B # 리모트 저장소 삭제
```

## branch
```shell
$ git branch AA  # branch 생성
$ git checkout AA   # AA 브랜치로 이동
$ git branch -vv    # 현재 브랜치 상태 확인
$ git branch -d AA  # 브랜치 삭제
$ git push origin --delete AA # 리모트 브랜치 AA 삭제
```

## syntax highlight
* abap ('*.abap')
* ada ('.adb', '.ads', '*.ada')
* ahk ('.ahk', '.ahkl')
* apacheconf ('.htaccess', 'apache.conf', 'apache2.conf')
* applescript ('*.applescript')
* as ('*.as')
* as3 ('*.as')
* asy ('*.asy')
* bash ('.sh', '.ksh', '.bash', '.ebuild', '*.eclass')
* bat ('.bat', '.cmd')
* befunge ('*.befunge')
* blitzmax ('*.bmx')
* boo ('*.boo')
* brainfuck ('.bf', '.b')
* c ('.c', '.h')
* cfm ('.cfm', '.cfml', '*.cfc')
* cheetah ('.tmpl', '.spt')
* cl ('.cl', '.lisp', '*.el')
* clojure ('.clj', '.cljs')
* cmake ('*.cmake', 'CMakeLists.txt')
* coffeescript ('*.coffee')
* console ('*.sh-session')
* control ('control')
* cpp ('.cpp', '.hpp', '.c++', '.h++', '.cc', '.hh', '.cxx', '.hxx', '*.pde')
* csharp ('*.cs')
* css ('*.css')
* cython ('.pyx', '.pxd', '*.pxi')
* d ('.d', '.di')
* delphi ('*.pas')
* diff ('.diff', '.patch')
* dpatch ('.dpatch', '.darcspatch')
* duel ('.duel', '.jbst')
* dylan ('.dylan', '.dyl')
* erb ('*.erb')
* erl ('*.erl-sh')
* erlang ('.erl', '.hrl')
* evoque ('*.evoque')
* factor ('*.factor')
* felix ('.flx', '.flxh')
* fortran ('.f', '.f90')
* gas ('.s', '.S')
* genshi ('*.kid')
* glsl ('.vert', '.frag', '*.geo')
* gnuplot ('.plot', '.plt')
* go ('*.go')
* groff ('.(1234567)', '.man')
* haml ('*.haml')
* haskell ('*.hs')
* html ('.html', '.htm', '.xhtml', '.xslt')
* hx ('*.hx')
* hybris ('.hy', '.hyb')
* ini ('.ini', '.cfg')
* io ('*.io')
* ioke ('*.ik')
* irc ('*.weechatlog')
* jade ('*.jade')
* java ('*.java')
* js ('*.js')
* jsp ('*.jsp')
* lhs ('*.lhs')
* llvm ('*.ll')
* logtalk ('*.lgt')
* lua ('.lua', '.wlua')
* make ('.mak', 'Makefile', 'makefile', 'Makefile.', 'GNUmakefile')
* mako ('*.mao')
* maql ('*.maql')
* mason ('.mhtml', '.mc', '*.mi', 'autohandler', 'dhandler')
* markdown ('*.md')
* modelica ('*.mo')
* modula2 ('.def', '.mod')
* moocode ('*.moo')
* mupad ('*.mu')
* mxml ('*.mxml')
* myghty ('*.myt', 'autodelegate')
* nasm ('.asm', '.ASM')
* newspeak ('*.ns2')
* objdump ('*.objdump')
* objectivec ('*.m')
* objectivej ('*.j')
* ocaml ('.ml', '.mli', '.mll', '.mly')
* ooc ('*.ooc')
* perl ('.pl', '.pm')
* php ('.php', '.php(345)')
* postscript ('.ps', '.eps')
* pot ('.pot', '.po')
* pov ('.pov', '.inc')
* prolog ('.prolog', '.pro', '*.pl')
* properties ('*.properties')
* protobuf ('*.proto')
* py3tb ('*.py3tb')
* pytb ('*.pytb')
* python ('.py', '.pyw', '.sc', 'SConstruct', 'SConscript', '.tac')
* r ('*.R')
* rb ('.rb', '.rbw', 'Rakefile', '.rake', '.gemspec', '.rbx', '.duby')
* rconsole ('*.Rout')
* rebol ('.r', '.r3')
* redcode ('*.cw')
* rhtml ('*.rhtml')
* rst ('.rst', '.rest')
* sass ('*.sass')
* scala ('*.scala')
* scaml ('*.scaml')
* scheme ('*.scm')
* scss ('*.scss')
* smalltalk ('*.st')
* smarty ('*.tpl')
* sourceslist ('sources.list')
* splus ('.S', '.R')
* sql ('*.sql')
* sqlite3 ('*.sqlite3-console')
* squidconf ('squid.conf')
* ssp ('*.ssp')
* tcl ('*.tcl')
* tcsh ('.tcsh', '.csh')
* tex ('.tex', '.aux', '*.toc')
* text ('*.txt')
* v ('.v', '.sv')
* vala ('.vala', '.vapi')
* vbnet ('.vb', '.bas')
* velocity ('.vm', '.fhtml')
* vim ('*.vim', '.vimrc')
* xml ('.xml', '.xsl', '.rss', '.xslt', '.xsd', '.wsdl')
* xquery ('.xqy', '.xquery')
* xslt ('.xsl', '.xslt')
* yaml ('.yaml', '.yml')


## git 삭제(mac)
find ./ -name ".git" | xargs rm -Rf
find ./ -name ".svn" | xargs rm -Rf
