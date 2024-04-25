Linux에서는 패키지를 설치할때 gcc/g++로 컴파일해야 했었음, 편의성을 위해
rpm(redhat package manager)이 등장하고, 이후 의존성관리를 좀 더 편리하게 할 수 있는 yum이 등장

## 사용법
```shell
$ yum list installed | grep 패키지명    # 설치된 패키지 검색
$ yum localinstall <url>    # url로 바로 설치
$ yum clean all # cache clear
$ yum remove 패키지명 # 패키지 삭제
```


## yum은 repository에서 패키지를 다운 받게됨
* repository 확인, 서버에 repository가 등록되어 있음
    ```shell
    $ yum repolist
    ```
    <img src="../../assets/yum_repolist.png"></img>
* repository가 등록되어 있는 위치   
    ```shell
    $ cd /etc/yum.repos.d/*.repo
    ```
    <img src="../../assets/etc_yum_repos_d.png"></img>
* 각각의 파일의 내용은 다음과 같다   
    ```shell
    $ cat vscode.repo
    ```
    <img src="../../assets/vscode_repo.png"></img>
    이름(name), URL(baseurl), 활성화여부(enabled), 유효성체크여부(gpgcheck), 키파일(gpgkey) 가 기록되어 있음
<hr>

##  offline용 repository 만들기

1. (인터넷망) yum-utils, createrepo를 설치한다
    ```shell
    $ yum install yum-utils
    $ yum install createrepo
    ```
2. (인터넷망) 설치 패키지 검색 (vim을 예로...)
    ```shell
    $ yum search vim    # 온라인 repository에서 설치할 패키지 검색
    
    Loaded plugins: fastestmirror
    Loading mirror speeds from cached hostfile
    ============================================================================================= N/S matched: vim =============================================================================================
    vim-common.x86_64 : The common files needed by any version of the VIM editor
    vim-enhanced.x86_64 : A version of the VIM editor which includes recent enhancements
    vim-filesystem.x86_64 : VIM filesystem layout
    vim-minimal.x86_64 : A minimal version of the VIM editor
    
    Name and summary matches only, use "search all" for everything.
    ```
    vim-enhanced.x86_64를 설치할 예정 

3. (인터넷망) 설치할 패키지 다운로드
    ```shell
    $ mkdir -P repos/vim-enhanced   # directory를 생성하고
    $ yumdownloader --downloadonly --resolve vim-enhanced   # 패키지 다운로드
    # --resolve : 의존성관련 전체
    # --downloadonly : 설치하지 않고 다운로드만
    
    Loaded plugins: fastestmirror
    Loading mirror speeds from cached hostfile
    * base: mirrors.cat.net
    * extras: mirrors.cat.net
    * updates: ftp-srv2.kddilabs.jp
    --> Running transaction check
    ---> Package vim-enhanced.x86_64 2:7.4.629-8.el7_9 will be installed
    --> Finished Dependency Resolution
    vim-enhanced-7.4.629-8.el7_9.x86_64.rpm                                                                                                                                              | 1.1 MB  00:00:01
    exiting because "Download Only" specified
    ```

4. (인터넷망) createrepo (상위 디렉토리에서 작업)

    ```shell
    $ createrepo vim-enhanced   # 대상 디렉토리에 createrepo
    Spawning worker 0 with 1 pkgs
    Workers Finished
    Saving Primary metadata
    Saving file lists metadata
    Saving other metadata
    Generating sqlite DBs
    Sqlite DBs complete
    ```

5. (인터넷망) repository 등록/테스트 (/etc/yum.repos.d/)
    ```shell
    $ ls -all
    합계 16
    drwxr-xr-x.  4 root root   59  9월 30 16:32 .
    drwxr-xr-x. 74 root root 8192  9월 30 15:13 ..
    drwxr-xr-x.  2 root root  220  9월 30 16:32 backup
    drwxr-xr-x.  2 root root    6  9월 30 16:32 custom
    -rw-r--r--.  1 root root   95  9월 30 16:30 vim-enhanced.repo
    
    $ cat vim-enhanced.repo  # repo 파일을 작성한다
    [vim-enhanced]
    name=vim enhanced
    baseurl=file:///APP/repos/vim-enhanced/
    enalbed=1
    gpgcheck=0
    
    $ yum repolist  # vim-enhanced가 보이면 정상
    Loaded plugins: fastestmirror
    Loading mirror speeds from cached hostfile
    repo id         repo name       status
    vim-enhanced    vim enhanced    1
    repolist: 1
    ```
6. (인터넷망) 파일을 압축하여 폐쇄망으로 이동
    ```shell
    $ tar zcvf repos.tar.gz /APP/repos /etc/yum.repos.d/vim-enhanced.repo
    ```
7. (폐쇄망) 
    ```shell
    $ tar -xvzf repos.tar.gz    # 압축해제
    $ mv vim-enhanced.repo /etc/yum.repos.d/    # repo파일 이동, 기존 repo 파일은 backup 해둔다
    $ yum -y install vim-enhanced   # 패키지를 설치한다
    ```

# Yum 사용법

## 기본 형태

기본적인 형태는 아래와 같다

```
# 옵션 - 명령어 - 패키지명 순으로 적는다.
yum <option> <command> <package_name>
```

## 패키지 검색

```shell
yum search nginx
```

## 패키지 설치

패키지를 설치하려면 다음과 같이하자.

```shell
# nginx 설치
yum install nginx
# 원하는 버전 설치
yum install nginx-18
```

보통 패키지를 설치할때 필요한 용량과 계속해서 진행할 지 물어보는 과정이 있는데 **-y 옵션을 주게되면 끊김 없이 진행할 수 있다.**

```
yum -y install nginx
```

## 패키지 업데이트

```shell
yum update nginx
```

## 패키지 삭제

의존성관리를 개별적으로 해줄 필요없이 삭제할 수 있다.

```shell
# nginx 삭제
yum remove nginx
```

## 서버에 있는 패키지 목록 확인

시스템에 설치된 패키지와 설치가능한 패키지의 목록을 출력한다.

```shell
yum list
```

## 설치된 패키지 확인

현재 시스템에 설치되어있는 패키지 리스트를 출력한다.

```shell
yum list installed
```

## 설치가능한 패키지 확인

시스템에 설치 가능한 패키지를 출력한다. 보통 grep과 같이 사용하곤 한다.

```
yum list available | grep <name>
```

## 업데이트가 필요한 패키지 확인

현재 시스템에 설치된 패키지들 중에서 업데이트가 필요한 패키지를 출력한다.

```shell
yum list updated
```

## 패키지 정보 확인

```shell
yum info <package_name>
```

