# 1. Django - MariaDB 연결

## settings.py 파일 수정

> [MariaDB notes](https://docs.djangoproject.com/en/4.1/ref/databases/#mariadb-notes)
>
> Django supports MariaDB 10.3 and higher. 
>
> To use MariaDB, **use the MySQL backend**, which is shared between the two. See the [MySQL notes](https://docs.djangoproject.com/en/4.1/ref/databases/#mysql-notes) for more details.

mariadb는 Mysql과 동일하게 적용하면 됨

```PYTHON
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'testdb',
        'USER': 'us_django',
        'PASSWORD': '1234',
        'PORT': '3306',
        'HOST': '192.168.56.103',
        'OPTIONS': {
            # 'init_command': "SET sql_mode='STRICT_TRANS_TABLES",		# 오류 발생
            'init_command': 'SET default_storage_engine=INNODB',			# 공식문서에 있는 내용으로 교체
        }
    }
}
```

> MariaDB, MySQL에는 Storage_engine을 설정 할 수 있게 되어 있는것 같음



## mysqlclient 1.4.6 버전 설치

django에서 MariaDB 연결을 위해 설치한다 (교제에서 사용한 버전을 참고 했으나 정확히 일치하지는 않는다)

```bash
(aws)  ~/workspace/python/bigdata_portal $ brew search mysql
==> Formulae
automysqlbackup          mysql-client             mysql-sandbox            mysql@5.7
mysql                    mysql-client@5.7         mysql-search-replace     mysqltuner
mysql++                  mysql-connector-c++      mysql@5.6                qt-mysql

(aws)  ~/workspace/python/bigdata_portal $ conda install mysqlclient=1.4.6
Collecting package metadata (current_repodata.json): done
Solving environment: failed with initial frozen solve. Retrying with flexible solve.
Collecting package metadata (repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 22.11.1
  latest version: 23.1.0

Please update conda by running

    $ conda update -n base -c defaults conda

Or to minimize the number of packages updated during conda update use

     conda install conda=23.1.0



## Package Plan ##

  environment location: /opt/anaconda3/envs/aws

  added / updated specs:
    - mysqlclient=1.4.6


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    ca-certificates-2023.01.10 |       hecd8cb5_0         121 KB
    mysql-connector-c-6.1.11   |       hccea1a4_1         1.2 MB
    mysqlclient-1.4.6          |   py36h0a44026_0          74 KB
    ------------------------------------------------------------
                                           Total:         1.4 MB

The following NEW packages will be INSTALLED:

  mysql-connector-c  pkgs/main/osx-64::mysql-connector-c-6.1.11-hccea1a4_1
  mysqlclient        pkgs/main/osx-64::mysqlclient-1.4.6-py36h0a44026_0

The following packages will be UPDATED:

  ca-certificates                     2022.10.11-hecd8cb5_0 --> 2023.01.10-hecd8cb5_0


Proceed ([y]/n)?  y


Downloading and Extracting Packages

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
```

## Migrate

runserver 실행 전 Migrate를 해줘야 오류가 발생하지 않는다

```bash
(aws)  ~/workspace/python/bigdata_portal/test_proj $ python manage.py migrate
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying admin.0003_logentry_add_action_flag_choices... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying auth.0008_alter_user_username_max_length... OK
  Applying auth.0009_alter_user_last_name_max_length... OK
  Applying sessions.0001_initial... OK
  
  
(aws)  ~/workspace/python/bigdata_portal/test_proj $ python manage.py runserver
Performing system checks...

System check identified no issues (0 silenced).
February 09, 2023 - 21:02:08
Django version 2.1.7, using settings 'test_proj.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
[09/Feb/2023 21:02:11] "GET / HTTP/1.1" 200 16348

```

# 2. MariaDB 확인

Migrate 후 여러개의 테이블이 생김

```mariadb
show tables;

auth_group
auth_group_permissions
auth_permission
auth_user
auth_user_groups
auth_user_user_permissions
django_admin_log
django_content_type
django_migrations
django_session
```

(교재)프로젝트에서는 auth 앱을 사용하며,  Django 기본 패키지 중 하나임

auth_user 테이블만 사용할 예정
