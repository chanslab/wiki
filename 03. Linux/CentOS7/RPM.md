## 사용법
```shell
$ rpm -Uvh 패키지명.rpm # 패키지 설치   
    -U : install or update   
    -v : 설치과정 확인
    -h : 설치과정을 '#' 기호로 화면에 출력
$ rpm -e 패키지명   # 패키지 삭제
$ rpm -qa | grep 패키지명 # 설치된 패키지 확인
$ rpm -qi 패키지명  # 설치된 패키지 상세정보 확인
$ rpm -qip 패키지명    # 아직 설치되지 않은 패키지의 상세정보 확인
$ rpm -ql 패키지명 # 설치된 패키지의 파일 경로 확인
$ rpm -qlp 패키지명 # 아직 설치되지 않은 패키지 파일 안의 경로 확인
$ rpm -qf /usr/bin/vim # 특정 파일을 설치 한 패키지 명 확인
```
## 옵션
|구분|옵션|추가옵션|설명|
|:---:|:---|:---|:---|
|설치|-i||패키지설치|
|||vh|v(verbose): 상세내역 출력, h(hash marks) : 프로그레스(#) 표시|
|||--nodeps|의존성 무시|
|||--replacepkgs|패키지 교체|
|||--replacefiles|패키지 파일 교체|
|||--force|강제설치|
|업그레이드|-U||패키지 업그레이드|
|||vh|v(verbose): 상세내역 출력, h(hash marks) : 프로그레스(#) 표시|
|||--nodeps|의존성 무시|
|||--replacepkgs|패키지 교체|
|||--replacefiles|패키지 파일 교체|
|||--force|강제 업그레이드|
|삭제|-e||패키지 삭제|
|||vh|v(verbose): 상세내역 출력, h(hash marks) : 프로그레스(#) 표시|
|||--nodeps|의존성 무시|
|||--test|실제 삭제하지 않고, 의존성 문제가 있는지 확인|





