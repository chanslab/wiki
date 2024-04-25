## tar, gzip

```shell
$ tar cvf AA.tar *  # 현재 디렉토리의 모든 파일과 디렉토리를 tar로 묶기
$ tar cvf AA.tar [PATH]  # 대상 디렉토리를 포함한 모든 파일과 디렉토리를 tar로 묶기
$ tar cvf AA.tar [file1][file2]  # 파일을 지정하여 tar로 묶기

$ tar xvf AA.tar  # 현재 디렉토리에 풀기
$ tar xvf AA.tar -C [PATH] # 지정된 디렉토리에 풀기
$ tar tvf AA.tar  # tar 아카이브의 내용 확인

$ tar zcvf AA.tar.gz *  # 현재 디렉토리를 tar로 묶고, gzip으로 압축하기
$ tar zxvf AA.tar.gz  # 현재 디렉토리에 풀기

$ tar jcvf AA.tar.bz2 *  # 현재 디렉토리를 tar로 묶고, bzip2으로 압축하기
$ tar jxvf AA.tar.bz2  # 현재 디렉토리에 풀기

$ tar cvfw AA.tar * # 파일별 진행 여부 확인하기
```

## linux 버전 확인

```shell
$ uname -a
```

## 사용자 Home directory 변경

```shell
$ cat /etc/passwd # 사용자 홈디렉토리 확인
$ usermod -d /(new)홈디렉토리 -m 사용자계정 # (new)홈디렉토리는 미리 생성 안해도 됨, -m 옵션으로 기존 홈디렉토리의 .bashrc와 같은 파일들도 모두 이동 
```

## Find 명령어

| 사용법                                        | 설명                                      |
|:------------------------------------------ |:--------------------------------------- |
| find                                       | 현재 디렉토리에 있는 파일 및 디렉토리 리스트 표시            |
| find [PATH]                                | 대상 디렉토리에 있는 파일 및 디렉토리 리스트 표시            |
| find . -name [FILE]                        | 현재 디렉토리 아래 모든 파일 및 하위 디렉토리에서 파일 검색      |
| find / -name [FILE]                        | 전체 시스템(루트 디렉토리)에서 파일 검색                 |
| find . -name "STR*"                        | 파일 이름이 특정 문자열로 시작하는 파일 검색               |
| find . -name "*STR*"                       | 파일 이름이 특정 문자열을 포함 파일 검색                 |
| find . -name "*STR"                        | 파일 이름이 특정 문자열로 끝나는 파일 검색                |
| find . -empty                              | 빈 디렉토리 또는 크기가 0인 파일 검색                  |
| find . -name "*.EXT" -delete               | 특정 확장자를 가진 모든 파일 검색 후 삭제                |
| find . -name [FILE] -print0                | 검색된 파일 리스트를 줄 바꿈 없이 이어서 출력하기            |
| find . -name [FILE] -type f                | 파일 또는 디렉토리만 검색하기                        |
| find . -size +[N]c -and -size -[M]c        | 파일 크기를 사용하여 파일 검색                       |
| find . -name [FILE] -exec ls -l {} \;      | 검색된 파일에 대한 상세 정보 출력. (find + ls)        |
| find . -name [FILE] -exec wc-l {} \;       | 검색된 파일의 라인 수 출력. (find + wc)            |
| find . -name [FILE] -exec grep "STR" {} \; | 검색된 파일에서 문자열 찾기. (find + grep)          |
| find . -name [FILE] > [SAVE_FILE]          | 검색 결과를 파일로 저장. (find, redirection)      |
| find . -name [FILE] 2> /dev/null           | 검색 중 에러 메시지 출력하지 않기 (find, redirection) |
| find . -maxdepth 1 -name [FILE]            | 하위 디렉토리 검색하지 않기                         |
| find . -name [FILE] -exec cp {} [PATH] \;  | 검색된 파일 복사. (find + cp)                  |
