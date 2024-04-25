# CentOS 자주 사용하는 명령어

[참고](https://jinwoo1990.github.io/dev-wiki/linux-command/)

## Linux 커맨드라인 사용법: [블로그](https://www.44bits.io/ko/post/linux-and-mac-command-line-survival-guide-for-beginner)



# 알아두면 좋은 리눅스 커맨드 - 사용법 및 예시

 May 6, 2021  14 minute read

데이터 분석을 하다보면 리눅스 커맨드를 사용할 일이 많이 생긴다. 본 포스트를 통해 자주 사용하는 리눅스 커맨드에 대해 알아보자. 포스트에 사용된 커맨드는 CentOS 8.3에서 테스트되었다. MacOS에서도 대부분의 리눅스 커맨드는 그대로 작동하며, 윈도우에서는 WSL2(Window Systems for Linux 2)을 통해 사용해 해볼 수 있다.

## Top 10

> cd

```
$ cd ..
$ cd ~
$ cd foo
$ cd foo/bar
$ cd /home/jin/foo/bar
```

`cd` 는 change directory의 약자로 디렉토리를 변경할 때 사용된다. `cd ..` 를 통해 상위 디렉토리로 이동하거나 `cd ~` 를 통해 사용자 홈 디렉토리로 이동할 수 있다. `cd foo/bar` 처럼 앞에 아무것도 붙이지 않으면 현재 디렉토리를 기준으로 디렉토리를 이동한다. `cd /home/jin/foo/bar` 처럼 절대경로를 지정해 디렉토리를 변경할 수도 있다.

> pwd

```
$ pwd
/home/jin
```

`pwd` 는 print working directory의 약자다. 말 그대로 현재 디렉토리를 출력한다.

> ls

```
# 한 줄 한 줄 출력
$ ls -l
# . 로 시작하는 숨김파일 보여줌
$ ls -al
```

`ls` 는 list segment의 약자다. 현재 디렉토리에 포함된 파일과 디렉토리를 나열한다. `ls` 만 입력하면 보기 불편해서 `ls -l` 을 통해 한 줄 한 줄 출력하는 형식을 많이 사용한다. 추가적으로 .gitignore, .env 같은 숨긴 파일들을 보기위해서는 -a 옵션을 추가해 `ls -al` 을 사용해야 한다. 대부분 `ls -al` 이 사용된다.

> mkdir

```
$ mkdir aa
$ mkdir -p bb/cc
```

make directory의 약자다. 디렉토리를 만들 때 사용된다. `-p` 옵션을 붙여주게 되면 디렉토리 안의 디렉토리도 만들 수 있다.

> touch

```
$ touch sample.txt
$ touch foo.py bar.py
```

`touch` 는 빈 파일을 만들 때 사용되는 커맨드이다. 복수개의 빈 파일 생성도 가능하다.

> mv

```
$ mv a.txt b.txt
$ mv a.txt /Users/jin/test/a.txt
```

`mv` 는 move의 약자다. 파일 이동 시 사용된다. 이동의 대상이 되는 파일은 없어지므로 이름을 바꾸는 용도로도 종종 사용된다.

> cp

```
$ cp c.txt d.txt
# 디렉토리 복사
$ cp -r dir_1 dir_2
```

`cp` 는 copy의 약자다. `mv`와 달리 `cp`의 대상이 되는 파일은 지워지지 않아 복사의 용도로 활용된다. `-r` 옵션을 쓴다면 디렉토리를 복사할 수도 있다.

> rm

```
$ rm
$ rm -r
# 읽기 전용 파일까지 삭제
$ rm -rf
```

`rm` 은 remove를 뜻한다. `rm` 을 옵션 없이 사용하면 파일을 삭제하는데 사용되고 `-r` 옵션과 함께 사용 시 디렉토리를 삭제한다. `rm -rf` 로 삭제하면 내부 디렉토리까지 합쳐서 읽기 전용 파일까지 강제로 삭제한다.

> cat

```
# 전체 출력
$ cat main.py
```

`cat` 은 concatnates의 약자다. 대상이 되는 파일 전체의 내용들을 합쳐서 출력하기에 붙여진 이름이다. 실제로는 특정 파일 내용을 출력하기 위해 사용된다.

> echo

```
$ echo "Hello world"
Hello world

$ echo $USER
jin

# 변수를 이용한 출력 
$ echo "Hello $USER"
Hello jin

# 이스케이프 문자를 적용해 $USER 를 문자 그대로 출력
$ echo "Hello \$USER"
Hello $USER

# $() - 명령어 결과를 이용해 출력
$ echo "Current directory is $(pwd)."
Current directory is /home/jin.

# 변수와 연결해서 특정 문자를 붙여 출력
$ echo "DB name is ${USER}_db"
DB name is jin_db

# $(()) - 계산 결과를 이용해 출력 
$ echo "1+2 == $((1+2))"
1+2 == 3

# ""가 아닌 ''를 사용 시 $변수를 문자 그대로 해석하므로 주의
$ echo 'Hello $USER'
Hello $USER
```

`echo` 는 문자열 출력을 위해 사용하는 리눅스 커맨드다. 여타 언어들의 `print`, `printf` 등과 비슷하다.

변수나 명령어 결과를 활용해 다양한 형태로 출력이 가능하다. 상세한 예시는 위를 참조하기 바란다.

## 패키지 관리자

> yum, apt-get

```
# yum
# 패키지 관리자 업데이트
$ yum update
# 설치
$ yum install python36
# 패키지 업데이트
$ yum update python36
# 패키지 삭제
$ yum remove python36

# apt-get
# 패키지 관리자 업데이트
$ apt-get update
# 설치
$ apt-get install python
# 패키지 업데이트
$ apt-get upgrade python
# 패키지 삭제
$ apt-get --purge remove python
```

`yum`과 `apt`는 패키지 설치를 위한 관리 툴이다. 윈도우의 경우 msi 인스톨러를 통해 GUI 환경에서 설치하게 되는데 유닉스 계열의 시스템들은 패키지 관리 툴을 이용해 필요한 소프트웨어를 설치한다. CentOS 같은 redhat 계열은 yum을 사용하고 Ubuntu 같은 debian 계열은 `apt`을 사용한다. 참고로 윈도우 WSL2는 `apt`, 맥은 경우는 `brew`를 이용한다.

## 환경변수 및 Alias

> env

```
$ env
LANG=en_US.UTF-8
HOSTNAME=b9z73q84a951
OLDPWD=/etc
USER=jin
PWD=/home/jin
HOME=/home/jin
PATH=/home/jin/.local/bin:/home/jin/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

`env` 를 통해 설정되어 있는 환경변수를 출력할 수 있다. 확인용으로 종종 쓰인다.

> export, unset

```
# 등록
$ export DB_NAME="postgresql"
$ echo DB name is $DB_NAME
DB name is postgresql
# 삭제
$ unset DB_NAME
$ echo DB name is $DB_NAME
DB name is 

# 기존 환경변수 활용해서 환경변수 수정
$ export PATH="$PYENV_ROOT/bin:$PATH"

# 일반변수 (쉘 스크립팅에서 활용)
$ DB_DEST="prd"
$ echo $DB_DEST
$ unset DB_DEST
```

환경변수는 로그인이나 쉘 실행 시점에 동적으로 정의된다. `export` 를 통해 전역으로 사용될 환경 변수를 지정할 수 있고 `unset` 을 통해 삭제가 가능하다.

쉘 실행 중에 설정한 환경변수들은 별도의 설정을 하지 않으면 쉘 종료 시 사라진다. `.bashrc` 나 `.bash_profile` 에 정의하면 쉘을 실행할 때 자동으로 설정되어 매번 `export` 할 필요가 없어진다. `.bashrc` 나 `bash_profile` 에 대한 자세한 내용은 뒤에 설명하겠다.

일반변수는 환경변수와 동일한 방법으로 생성하고 삭제할 수 있고 주로 쉘 스크립팅에서 활용된다.

> alias

```
# alias 확인
$ alias
# 등록
$ alias mycommand="mkdir myfolder"
# 물론 이렇게 등록한 alias는 터미널 끄면 없어짐
$ unalias mycommand
# .bashrc나 .zshrc에 alias 추가
$ alias mycommand="mkdir myfolder" >> ~/.bashrc
$ source ~/.bashrc
# ssh 접속 위한 alias
$ alias ec2_jin="ssh -i .ssh/ec2_jin.pem jin@23.54.174.391"
$ ec2_jin
```

`alias` 는 ‘가명’ 등의 의미로 컴퓨터에서는 ‘단축 명령어’ 정도로 생각하면 된다. 자주 쓰는 커맨드나 너무 길어 사용이 불편한 커맨드는 `alias` 로 등록해 사용한다. 예시는 위와 같다.

## 시스템 모니터링

> top, ps

```
# 시스템 사용 상황 출력
$ top
# ax 는 모든 프로세스 출력, u는 사용자 정보 출력
$ ps aux
# -e 는 커널 프로세스 제외 모든 프로세스 출력, -f 는 UID, PPID 등 추가 출력
$ ps -ef
```

시스템을 관리하다보면 프로세스들의 서버 사용 상황을 모니터링하고 싶을 때가 있다. 윈도우 작업관리자처럼 `top` 은 프로세스별 메모리, CPU 사용 상황을 보여준다. `ps aux` 와 `ps -ef` 도 비슷한 기능을 한다.

> kill

```
# 종료 (종료 과정에 문제 생기면 프로세스 남아 있음)
$ kill <PID>
# 강제 종료
$ kill -9 <PID>
```

실질적으로 `top` , `ps` 와 같이 쓰인다. `top` 이나 `ps` 로 프로세스들을 확인해봤을 때 특정 프로세스가 메모리나 CPU 사용에서 문제를 일으키고 있거나 멈췄다면 `kill` 을 사용해 강제종료한다. 데이터 분석 작업을 하다가도 가끔 서버를 건드릴 일이 생기는데 `top` 과 `kill -9 <PID>` 정도는 상식으로 알아두면 분명 쓰일 때가 생길 것이다.

## 다운로드

> wget, curl

```
# wget은 yum install wget 으로 설치 필요
# 아무 인자가 없으면 / 뒤 이름으로 파일저장. -O 옵션으로 다운로드 받을 파일이름 지정 가능
$ wget https://downloads.python.org/pypy/pypy3.7-v7.3.4-linux64.tar.bz2
$ wget -O pypy3.7.tar.bz2 https://downloads.python.org/pypy/pypy3.7-v7.3.4-linux64.tar.bz2

# curl은 대문자 O가 마지막 / 뒤 이름으로 파일저장이고 소문자 o가 지정한 이름으로 파일저장임  
$ curl -O https://downloads.python.org/pypy/pypy3.7-v7.3.4-linux64.tar.bz2
$ curl -o pypy3.7.tar.bz2 https://downloads.python.org/pypy/pypy3.7-v7.3.4-linux64.tar.bz2
```

`wget` 과 `curl` 은 외부 네트워크에서 파일을 다운로드 받을 때 많이 쓴다. `https` 를 활용해 다운받는 대다수의 케이스에서는 두 개의 사용에 큰 차이가 없다. `wget` 이 조금 더 직관적이고 `curl` 은 기능이 더 많다.

옵션을 통해 다운로드할 파일의 이름을 지정할 수 있다.

> tar

```
$ yum install bzip2
$ yum install gzip

# 압축풀기
$ tar xvf A.tar
$ tar zxvf A.tar.gz
$ tar jxvf A.tar.bz2
# 예시
$ tar jxvf pypy3.7-v7.3.4-linux64.tar.bz2

# 압축방법
$ tar cvf A.tar my_folder
$ tar zcvf A.tar.gz my_folder
$ tar jcvf A.tar.gz my_folder

# 내용 확인
$ tar tvf A.tar

# 파일 확인
$ file pypy3.7-v7.3.4-linux64.tar.bz2
```

`tar` 은 압축 파일을 다룰 때 쓰인다. `wget` 과 `curl` 로 받은 다운로드 파일의 압축을 풀거나 배포 등의 이유로 압축을 직접 수행해야 할 때 쓰인다.

압축을 할 때는 `tar` 은 파일들을 묶는 기능만 수행하고 `gzip` 이나 `bzip2` 가 데이터의 크기를 줄이는 압축을한다. `tar` 로 압축을 하면 `.tar` 이 붙으며 파일들이 모아지고 그 후 `.gz` 나 `.bz2` 가 붙으며 압축이 되어 데이터 크기가 줄어든다.

옵션을 사용해 원하는 방식으로 압축을 하거나 풀 수 있다. 파일 확장자를 보고 확장자에 맞는 옵션을 써서 압축을 풀 수 있다. 압축을 풀려고 할 때 에러가 난다면 `file` 명령어를 사용해 확장자와 다른 방식으로 압축된 파일인지 확인해보자.

> make

```
# make 설치
$ yum udpate && yum install make

$ tar xvzf foo.tar.gz
$ cd directory_name
$ ./configure
$ make
$ make install
```

압축 풀었을 때 실행할 수 있는 바이너리 파일로 컴파일이 안 되있다면 `make` 를 통해 컴파일을 해야 한다. `make` 는 Makefile에 있는 C 컴파일 순서에 따라 컴파일을 진행해 사용자가 사용할 수 있는 바이너리 파일을 만든다.

불가피하게 `yum` 같은 패키지 관리자를 통해 설치하지 못하거나 오류 등으로 인해 직접 깔아야 할 경우에 이렇게라도 대략적인 방법을 알아두면 나중에 유용하게 쓸 수 있을 것이다.

## 소유권 및 허가권

> useradd, usedel, usermod, passwd, groupadd, groupdel, gpasswd

```
$ useradd jin
# 작동안하면 yum install passwd
$ passwd jin
$ userdel -rf jin

# 1001 은 GID, 없으면 1000번부터 순차적으로 생성됨
$ groupadd -g 1020 group1
$ groupdel group1

# 그룹과 함께 useradd
$ useradd -g group1 woo

# 그룹에 사용자 추가
$ gpasswd -a jin group1
# 그룹에 사용자 삭제
$ gpasswd -d jin group1

# 그룹 관리자 지정 (관리자로 지정되면 해당 계정에서 group 사용자 추가, 삭제 가능)
$ gpasswd -A jin group1

# 사용자 목록 확인
$ cat /etc/passwd

# 그룹 목록 확인
$ cat /etc/group

# 정보 조회
$ id jin
$ groups jin

# 그룹 변경
$ usermod -g group2 jin

# 쉘 사용자 변경
$ su jin
```

리눅스는 다중사용자 시스템으로 사용자와 그룹이 존재한다. 리눅스 시스템은 사용자와 그룹별로 권한을 관리하며 이를 통해 파일을 읽고, 쓰고, 실행한다.

시스템 관리 시에는 그룹에 권한을 부여하고 사용자를 그룹에 할당해 파일이나 디렉토리의 접근을 관리한다.

위 예시는 사용자 및 그룹의 추가, 삭제, 변경에 대한 커맨드들이다.

> chown

```
# 사용자 권한 변경. -R 은 하위 파일, 디렉토리 권한까지 변경
$ chown jin file.py
$ chown jin mydirectory
$ chown jin -R mydirectory

# 그룹 권한 변경. -R 은 하위 파일, 디렉토리 권한까지 변경
$ chown group1 file.py
$ chown group1 mydirectory
$ chown group1 -R mydirectory

# 사용자, 그룹 권한 동시 변경. -R 은 하위 파일, 디렉토리 권한까지 변경
$ chown jin:group1 file.py
$ chown jin:group1 mydirectory
$ chown jin:group1 -R mydirectory

# 세번째 컬럼이 소유 사용자, 네번째 컬럼이 소유 그룹
$ ls -al
drwxr-xr-x 2 jin  group1   4096 May  6 02:35 test2
```

사용자와 그룹을 만들면 이를 바탕으로 파일이나 디렉토리에 소유권(ownership)을 정할 수 있다. `chown` 은 파일이나 디렉토리의 소유권을 변경해 추후 허가권(permission)을 적용할 방법을 정의한다.

사용자 변경, 그룹 변경, 동시 변경 모두 가능하며 `-R` 옵션을 통해 하위 디렉토리의 권한도 함께 변경 가능하다.

> chmod

```
$ ls -al
drwxr-xr-x 2 jin group1 4096 May  6 02:44 aa
-rw-r--r-- 1 jin group1    4 May  6 02:47 c

# 사용자에게 rwx 권한, 사용자 그룹에 rwx 권한, 다른 그룹에 rwx 권한 부여
$ chmod 777 test.sh
# 사용자에게 rwx 권한, 사용자 그룹에 rwx 권한, 다른 그룹에 r-x 권한 부여
$ chmod 775 test.sh
# 사용자에게 rwx 권한, 사용자 그룹에 r-- 권한, 다른 그룹에 r-- 권한 부여
$ chmod 744 test.sh

# 모든 사용자에 대해 실행 권한 부여
$ chmod +x test.sh
# 모든 사용자에 대해 실행 권한 제거
$ chmod -x test.sh
```

`chmod` 는 파일이나 디렉토리에 대한 허가권을 변경한다. `chmod 775 test.sh` 나 `chmod +x test.sh` 같은 형식으로 허가권을 변경하면 소유자, 그룹, 타 그룹별로 허가권이 설정된다.

허가권에 대한 내용을 간단히 정리하면 아래와 같다.

- 파일권한은 총 10글자로 이루어져있다. (e.g. drwxr-xr-x)
- 첫번째 글자는 `d`, `-`, `l` 로 구성된다. `d` 는 directory, `-` 는 파일, `l` 은 심볼릭 링크를 의미한다.
- 그 다음 9글자는 실제 파일 권한을 나타낸다. 첫번째 3글자는 소유자의 권한, 다음 3글자는 소유 그룹의 권한, 그 다음 3글자는 다른 그룹의 권한을 의미한다.
- 권한은 `r`, `w`, `x` 로 나타내며 각각 읽기, 쓰기, 실행을 뜻한다.
- chmod를 통해 숫자로 권한을 바꿀 수 있다.
  - 읽기(4), 쓰기(2), 실행(1) 을 더한 숫자로 권한 변경 (e.g. 4+2+1 은 7로 7을 주면 모든 권한을 가짐)

참고로 기본적으로 파일은 실행권한이 없이 만들어지고 실행권한을 줘야 `./test.sh` 나 `source test.sh` 로 실행이 가능하다. 개발하며 `.githooks` 등을 다룰 때 실행권한을 주며 파일을 다루게 된다.

## 알아두면 좋은 다른 커맨드

> man, -h, —help

```
$ man cp
$ grep -h
# 아래처럼 작동 안할 때도 있고 -h 가 별도의 옵션일 수도 있음 
$ mv -h
# 아예 없을 것 같은 옵션 실행시켜서 무슨 옵션 있나 보는 방법도 있음
$ mv -qwqeesdf
```

커맨드의 사용법을 확인하고 싶을 때가 있다. `man` 은 manual의 약자로 대상이 되는 커맨드에 대한 매뉴얼 문서를 보여준다.

`man` 으로 보여지는 매뉴얼 문서가 너무 복잡해서 간단히 옵션 사용법 정도만 보고 싶다면 커맨드에 `-h` 나 `--help` 옵션을 붙여서 확인해보면 된다. 어떤 커맨드들은 해당 옵션이 구현되어있지 않기도 하는데 이럴 때는 아예 없을 것 같은 옵션을 실행시켜보거나 검색을 해보면 된다.

만약 docker로 centOS를 띄웠을 시 `yum install man` 을 해도 `man` 커맨드가 작동하지 않을 수 있다. locale 문제인데 해결방법이 조금 복잡하다. https://stackoverflow.com/questions/28405902/how-to-set-the-locale-inside-a-debian-ubuntu-docker-container 를 참조해서 고쳐보기 바란다. 직접 처음부터 끝까지 서버를 구성하는 것이 아니라면 이런 설정들은 되어 있으니 커맨드 사용법만 익히려면 macOS나 WSL2에서 테스트만해봐도 무방하다.

> head, tail

```
# 앞부분 출력 (기본 10줄)
$ head -n 5 main.py
$ head -5 main.py
# 뒷부분 출력 (기본 10줄)
$ tail -n 5 main.py
$ tail -5 main.py
# 프로그램 종료하지 않고 업데이트 되는 내용 출력
$ tail -f log.txt
```

`head` 와 `tail` 은 전체 내용을 출력하지 않고 앞부분이나 뒷부분의 내용을 원하는 줄 수만큼 지정해 출력한다. 원하는 내용이 앞쪽이나 뒷쪽에 있을 때 `cat` 보다 활용하기 편리하다.

`tail -f log.txt` 로 특정 파일에 업데이트 되는 내용을 쉘에 출력할 수 있는데, 로그 파일에 추가되는 사항들을 모니터할 때 사용할 수 있다.

> history

```
$ history
		1  cd ..
    2  cd ~
    3  pwd
    4  touch a b c
    5  mkdir test
    6  ls -al
# 2번 history에 있는 커맨드 입력 (cd ~ 실행됨)
$ !2
```

보통 키보드 위쪽 방향키로 이전에 사용한 커맨드를 찾아쓰기도 하지만 실행된 커맨드가 많을 때 `history` 를 이용하면 편리하다. 여태껏 실행한 커맨드들이 나오고 `!number` 의 형태로 예전 커맨드를 불러올 수 있다.

> which

```
$ which python
$ which docker
$ which brew
```

`which` 는 프로그램의 위치를 확인할 때 사용된다. 실제 실행 파일의 위치가 어디있는 지 알아야 할 때 종종 쓰인다.

> ln

```
# 심볼릭 링크
$ ln -s original copy
# 심볼릭 링크 삭제
$ rm copy
# 예시
$ ls -al
lrwxrwxrwx   1 root root    7 Nov  3  2020 bin -> usr/bin
```

심볼릭 링크를 설정하면 생성, 수정, 삭제 등 모든 행위가 공유된다. `ls -al` 을 쳤을 때 `->` 로 표시되는 항목들이 심볼릭 링크에 해당한다. 많은 커맨드들과 프로그램들이 심볼릭 링크를 사용해 기능에 접근할 수 있게 만들어져 있다. 자주 쓴다기보다는 알아두면 좋은 개념이다.

## 리다이렉션 및 다중명령어

> \>, », <

```
# > 는 기존 파일의 내용을 표준 출력으로 덮어씀 
$ echo "Hello world!" > hello.txt
$ echo "Goodbye world!" > hello.txt

# >> 는 기존 파일 내용 아래에 표준 출력을 추가함
$ echo "This is first line" >> example.txt
$ echo "This is second line" >> example.txt
```

리눅스에서는 `>` , `>>` 를 조합해 출력을 다른 곳으로 리다이렉션할 수 있다. `>` 는 좌항의 출력을 우항의 파일로 덮어씌우고 `>>` 는 좌항의 출력을 우항의 파일에 추가한다.

```
# 내용을 넘겨줄 수도 있음
$ cat < example.txt
```

반대로 좌항의 커맨드에 파일을 넘겨줄 수도 있다.

```
$ cat log_20300505.txt > log.txt
cd: no such file or directory: jin
# > 나 >> 앞에 2를 붙여주면 STDERR(에러 내용)을 리다이렉션
$ cat log_20300505.txt 2>> log.txt
```

`>` 나 `>>` 를 그냥 쓰면 표준출력(STDOUT)이 리다이렉션된다. 표준에러(STDERR)는 에러가 나왔을 때 나오는 결과로 표준출력과 접근방법이 다르다. `>` 나 `>>` 앞에 `2` 를 붙이면 표준출력 대신 표준에러를 리다이렉션해준다.

```
$ cat log_20300505.txt >> log.txt 2>&1
$ cat log_20210505.txt
# crontab 사용 로그 생성 예시
$ * */10 * * * /home/jin/toy_corona/venv/bin/python /home/jin/toy_corona/parser.py >> /home/jin/toy_corona/crawl_seoul.log 2>&1
```

리다이렉션은 배치 로그 설계에 활용될 수 있다. `>>` 로 리다이렉션 후 마지막에 `2>&1` 을 붙여주면 표준출력과 표준에러를 모두 기록한다.

> 파이프 (|)

```
$ history | tail -3
$ cat main.py | grep import
```

파이프(`|`)는 명령어를 조합해서 사용하기 위해 쓰인다. 좌항의 커맨드 내용을 받아 `tail` , `grep` 등의 커맨드로 필터링을 하는 등의 방식으로 활용된다.

> 다중명령어 (;, &&, &, ||)

```
# ; 는 앞의 명령어가 실패해도 다음 명령어를 실행
$ cd config; find *.py
# && 은 앞의 명령어가 성공해야 뒤의 명령어를 실행
$ cd config && find *.py
# & 는 명령어를 백그라운드로 실행 (config로 이동이 백그라운드로 이루어져 config 디렉토리가 아닌 현재 디렉토리에서 py 파일을 찾음)
$ cd config & find *.py
# || 는 앞 명령어가 성공하면 그 후 명령어를 실행하지 않음 (config로 이동이 성공하면 find가 실행되지 않음)
$ cd config || find *.py
```

편의성이나 테스트 등의 목적으로 한 번에 여러가지 리눅스 커맨드를 작성해야 될 경우가 있다. `;`, `&&`, `&`, `||` 는 각각 다른 방식으로 다중명령어를 수행한다.

## 쉘 설정파일

```
/etc/profile
/etc/bashrc
~/.bash_profile
~/.bashrc
~/.bash_logout
```

우리가 사용하는 리눅스 커맨드는 쉘 설정파일의 설정과 함수들의 도움을 받아 실행된다.

쉘 설정파일은 총 5개가 존재하는데, 전역파일 2개는 /etc 아래에 위치하고 사용자별 설정파일 3개는 ~ 아래에 위치한다.

쉘 설정파일은 쉘을 열 때마다 실행되며 환경변수나 alias를 등록하고 정의된 함수를 동작시킨다. 설정파일들의 실행순서는 다음과 같다.

- 실행순서: `/etc/profile` → `~/.bash_profile` → `~/.bashrc` → `~/etc/bashrc` → `~/.bash_logout`

이 때 `profile` 은 로그인할 때만 수행되고 (e.g. SSH로 id, password를 치고 접근, su로 user 변경) `.bashrc` 는 쉘을 열 때마다 항상 수행된다.

사용자 관점에서 보면 `.bash_profile` 과 `.bashrc` 에 환경변수와 alias, 함수를 정의해놓고 쓰면 된다. 일반적으로 `.bash_profile` 에 환경변수 입력, `.bashrc` 에 alias, 사용자 정의 함수를 입력한다. 만약 모든 사용자에게 설정을 적용하고 싶으면 `/etc/bashrc` 와 `/etc/profile` 을 이용하면 된다.

파일별 설정이 헷갈리면 `.bashrc` 에 모든 설정을 입력해도 작동에 지장은 없다. 바꾼 내용을 해당 쉘에서 바로 적용하고 싶으면 `source ~./bashrc` 를 사용하도록 하자. 한 번 `source` 를 하거나 다시 쉘을 실행시키면 그 다음부터는 `source` 커맨드는 사용하지 않아도 된다.

## 기타

> 옵션

```
$ grep -h
$ grep --help
$ rm -rf
```

앞선 커맨드들의 예시에서 나왔지만 옵션이 문자 하나인 경우에는 `-` 를 사용하고 두 글자 이상일 경우는 `--` 를 사용한다. 또, `-` 에는 `rmf -rf` 처럼 여러 개 옵션 지정이 가능하다.

> CentOS, Ubuntu 버전 확인

```
# CentOS
$ cat /etc/redhat-release
# Ubuntu
$ cat /etc/lsb-release
```

버전을 확인하고 싶을 때 쓸 수 있다.

> 멀티라인

```
$ echo hello \
> world
```

공백없이 라인 끝에 `\` 를 쓰면 멀티라인으로 입력이 가능하다.

