## 서버교체시 터미널에서 ssh 접속오류
```shell
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ECDSA key sent by the remote host is
SHA256:ZgpcIh+K1KmIze2c/bSwP4Z6sbQlXrqxU/hQLIA+4yA.
Please contact your system administrator.
Add correct host key in /Users/chan/.ssh/known_hosts to get rid of this message.
Offending ECDSA key in /Users/chan/.ssh/known_hosts:1
ECDSA host key for 192.168.56.101 has changed and you have requested strict checking.
Host key verification failed.
```
```shell
$ sudo ssh-keygen -R 192.168.56.101 # key값 갱신 (실행되지 않음)
$ vi ~/.ssh/known_hosts # 해당 서버 값을 지운다

$ cat known_hosts | grep 192.168.56.101 # key가 잡혀있다.
kcwbignn01t,192.168.56.101 ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBFRP8a8XuTlS5JOvB5Q1Al3qjKctRQFNh/Y+LtY7dOsb4zOsnQEd2U4DKiY/g50YX8+Dkh5jiV8tfOnqH2R1hwY=

$ ssh root@kcwbignn01t  # 해당 key값을 지우고 다시 접속, known_hosts에 다시 등록한다
The authenticity of host 'kcwbignn01t (192.168.56.101)' can't be established.
ECDSA key fingerprint is SHA256:ZgpcIh+K1KmIze2c/bSwP4Z6sbQlXrqxU/hQLIA+4yA.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'kcwbignn01t,192.168.56.101' (ECDSA) to the list of known hosts.


$ root@kcwbignn01t's password:      # 접속완료
Last login: Wed Sep 29 23:44:25 2021    

```