# Mysql character-set 설정



> UTF-8 문자 집합은 1~4바이트까지 저장이 가능하게 설계됨(가변 바이트)
>
> mysql/mariadb 에서는 전세계 모든 언어가 21bit(3바이트 조금 안됨)에 저장되기 때문에 utf8을 3바이트 가변 자료형으로 설계
>
> 따라서, 최근 나온 4바이트 문자열(Emoji 같은 것)을 utf8에 저장하면 값이 손실되는 현상이 발생 함

> 그래서, mysql에서 가변 4바이트 UTF-8 문자열을 저장할 수 있는 자료형을 추가 함 => utf8mb4

### Collation (정렬방식) 

> 텍스트 데이터를 정렬(ORDER BY) 할 때 사용, text 계열 자료형에서만 사용할 수 있는 속성

|                                               |                                                              | 예                      |
| --------------------------------------------- | ------------------------------------------------------------ | ----------------------- |
| utf8_bin (or utf8mb4_bin)                     | 바이너리 저장 값 그대로 정렬<br />hex 코드를 따른다. A(41), B(42), a(61), b(62) | A , B, a, b 식으로 정렬 |
| utf8_general_ci <br />(or utf8mb4_general_ci) | 바이너리를 한번 가공한 것<br />a 다음에 b 를 둔다는 라틴계열 문자를 사람의 인식에 맞게 정렬<br />일반적으로 널리 사용됨 | A, a, B, b 식으로 정렬  |
| utf8_unicode_ci<br />(or utf8mb4_unicode_ci)  | general_ci 보다 조금 더 사람에 맞게 정렬<br />한국어, 영어, 일본어, 중국어 사용환경에서는 general_ci 와 unicode_ci의 결과가 동일 | a, à, b, jośe, jose     |

### 권장하는 charset과 collation 설정 값

| mysql 버전 | character set | collation          |
| ---------- | ------------- | ------------------ |
| 5.5.3 이전 | utf8          | utf8_general_ci    |
| 최신 버전  | utf8mb4       | utf8mb4_unicode_ci |



### CentOS - mysql charset , collation 설정 값 변경

```
mysql> show variables like '%character%';
+--------------------------+--------------------------------+
| Variable_name            | Value                          |
+--------------------------+--------------------------------+
| character_set_client     | utf8                           |
| character_set_connection | utf8                           |
| character_set_database   | utf8                           |
| character_set_filesystem | binary                         |
| character_set_results    | utf8                           |
| character_set_server     | utf8                           |
| character_set_system     | utf8                           |
| character_sets_dir       | /var/lib/mysql/share/charsets/ |
+--------------------------+--------------------------------+
8 rows in set (0.00 sec)

mysql> show variables like '%collation%';
+----------------------+-----------------+
| Variable_name        | Value           |
+----------------------+-----------------+
| collation_connection | utf8_general_ci |
| collation_database   | utf8_general_ci |
| collation_server     | utf8_general_ci |
+----------------------+-----------------+
3 rows in set (0.00 sec)
```

