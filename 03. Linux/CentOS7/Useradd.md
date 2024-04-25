# 사용자 추가 

```shell
sudo useradd -m newuser

-- 옵션 -- 
-m : 해당 유저의 폴더를 같이 생성
-g : 그룹 지정
-d : 디렉토리 지정
-s : 쉘(shell) 지정
-p : 패스워드(암호) 지정
```

### 비밀번호 설정

```shell
sudo passwd newuser
# sudo passwd test
```



# 사용자 삭제

```shell
cat /etc/passwd

sudo userdel -r 계정
# sudo userdel -r test
```

# 사용자 확인

```shell
/etc/passwd
```

