## Homebrew 설치   

```shell
$ xcode-select --install    # Xcode Command line tool 설치
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"    # Homebrew 설치
$ brew -v   # 설치 확인
```

## Package 검색
Homebrew에서 패키지는 formula라고 부름   
패키지 브라우저 formulae : 
https://formulae.brew.sh/analytics 
```shell
$ brew search 패키지명  # 패키지 검색
$ brew install 패키지명 # 패키지 설치
$ brew outdated # 버전업된 패키지 확인
$ brew upgrade 패키지명    # 패키지 업그레이드
$ brew upgrade  # 모든 패키지 업그레이드
$ brew cleanup 패키지명 # 최신 버전의 패키지만 남겨두고 이전 버전 패키지는 삭제하기
$ brew uninstall 패키지명 # 패키지 삭제
```

## Package 관리
```shell
$ brew list # 설치한 패키지 목록 보기
$ brew info 패키지명    # 패키지 정보 보기
$ brew doctor   # 시스템 에러가 발생할 경우 확인
```

## Homebrew 업데이트 및 삭제
```shell
$ brew update   # 전체 update
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall)"   # Homebrew 삭제     
```