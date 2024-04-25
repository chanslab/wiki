# system_time_zone 변경

[TOC]

* mysql 은 서버의 timezone을 따른다
* my.cnf에 default_time_zone을 설정하거나 runtime의 time_zone 에 timezone을 변경해도 @@system_time_zone은 변경되지 않는다

### @@system_time_zone 확인

```sql
mysql> select @@system_time_zone;
+--------------------+
| @@system_time_zone |
+--------------------+
| EST                |
+--------------------+
1 row in set (0.00 sec)
```

##### @@system_time_zone을 변경하려면, CentOS의 timezone을 변경해야 한다

------

### CentOS7 timezone 조회

```bash
[root@kcwbigsv01t mysql]# date
2023. 02. 09. (목) 01:17:30 EST
[root@kcwbigsv01t mysql]# timedatectl
      Local time: 목 2023-02-09 01:18:58 EST
  Universal time: 목 2023-02-09 06:18:58 UTC
        RTC time: 목 2023-02-09 04:43:33
       Time zone: America/New_York (EST, -0500)
     NTP enabled: yes
NTP synchronized: yes
 RTC in local TZ: no
      DST active: no
 Last DST change: DST ended at
                  일 2022-11-06 01:59:59 EDT
                  일 2022-11-06 01:00:00 EST
 Next DST change: DST begins (the clock jumps one hour forward) at
                  일 2023-03-12 01:59:59 EST
                  일 2023-03-12 03:00:00 EDT
```

##### - date : local time 조회

##### - timedatectl : timezone 조회

##### - 위 명령어 모두 /etc/localtime 심볼릭 링크가 가리키고 있는 타임존에 의해 출력 됨

------

### timezone 변경

##### timedatectl을 이용하여 변경 (/etc/localtime의 심볼릭 링크를 변경하는 것)

##### timezone 목록 확인

```bash
[root@kcwbigsv01t mysql]# timedatectl list-timezones | grep -i seoul
Asia/Seoul
```

##### set-timezone 을 이용하여 변경

```bash
[root@kcwbigsv01t mysql]# timedatectl set-timezone Asia/Seoul
[root@kcwbigsv01t mysql]# timedatectl
      Local time: 목 2023-02-09 15:44:53 KST
  Universal time: 목 2023-02-09 06:44:53 UTC
        RTC time: 목 2023-02-09 04:47:36
       Time zone: Asia/Seoul (KST, +0900)
     NTP enabled: yes
NTP synchronized: no
 RTC in local TZ: no
      DST active: n/a
```

##### /etc/localtime 심볼릭 링크 확인

```bash
[root@kcwbigsv01t mysql]# ll /etc/localtime
lrwxrwxrwx. 1 root root 32  2월  9 15:44 /etc/localtime -> ../usr/share/zoneinfo/Asia/Seoul
```

###### /etc/localtime은 텍스트형 데이터가 아니기 때문에 vim 명령어로 읽어 들일 수 없음

###### zdump 명령어를 이용해 timezone을 읽을 수 있음

```bash
[root@kcwbigsv01t mysql]# zdump /etc/localtime
/etc/localtime  Thu Feb  9 15:52:22 2023 KST
[root@kcwbigsv01t mysql]# zdump /usr/share/zoneinfo/Asia/Seoul
/usr/share/zoneinfo/Asia/Seoul  Thu Feb  9 15:52:49 2023 KST
```

------

### Mysql 재시작 후 타임존 변경 확인

```sql
mysql> select @@system_time_zone;
+--------------------+
| @@system_time_zone |
+--------------------+
| KST                |
+--------------------+
1 row in set (0.00 sec)
```

