# Django Framework 

[TOC]

## 프로젝트 생성

```bash
(aws)  ~/workspace/python/bigdata_portal$ django-admin startproject test_proj
(aws)  ~/workspace/python/bigdata_portal$ tree test_proj
test_proj
├── manage.py
└── test_proj
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```

------

## 프로젝트 예제 실행

### 프로젝트 실행전 migrate 명령 실행

```bash
# 프로젝트 디렉토리 안의 manage.py 파일이 있는 위치에서 실행
(aws)  ~/workspace/python/bigdata_portal/test_proj$ python manage.py migrate
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
```

### 프로젝트 실행

```bash
(aws)  ~/workspace/python/bigdata_portal/test_proj$ python manage.py runserver
Performing system checks...

System check identified no issues (0 silenced).
February 09, 2023 - 01:50:49
Django version 2.1.7, using settings 'test_proj.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```

<img src="img/스크린샷 2023-02-09 오전 8.57.53.png" style="zoom: 25%;" />

------

## 프로젝트 기본 구조

```bash
test_proj																					# Project 포함 디렉토리
├── db.sqlite3																		# SQLite DB 파일
├── manage.py																			# Django 프로젝트 실행 파일
└── test_proj                                     # Project 디렉토리
    ├── __init__.py																# Python 패키지 디렉토리임을 명시
    ├── __pycache__																# Python3 Compile 디렉토리
    │   ├── __init__.cpython-36.pyc
    │   ├── settings.cpython-36.pyc
    │   ├── urls.cpython-36.pyc
    │   └── wsgi.cpython-36.pyc
    ├── settings.py																# Django 프로젝트 파일
    ├── urls.py																		# Django 프로젝트 URL 명시 파일
    └── wsgi.py																		# Django 웹 서비스 호환 파일

3 directories, 10 files
```

------

### Django 앱(App)

#### 앱 생성 (startapp)

```bash
(aws)  ~/workspace/python/bigdata_portal/test_proj$ python manage.py startapp testapp
(aws)  ~/workspace/python/bigdata_portal/test_proj$ tree
└── testapp																				# 앱 루트 디렉토리
    ├── __init__.py																# python 패키지 명시 파일
    ├── admin.py																	# 앱 관리자 페이지 등록 Model 정보	
    ├── apps.py																		# 앱 실행시 초기 실행 등 설정 파일
    ├── migrations																# 앱 내 Model 갱신시 사용
    │   └── __init__.py
    ├── models.py																	# 앱 Model 정보
    ├── tests.py																	# 앱 Test 페이지 파일
    └── views.py																	# 앱 View 정보
```

------

## settings.py

| 항목                     | 설명                                                         | 비고                                                         |
| ------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| SECRET_KEY               | 외부로부터 접근시 해당 key값을 모르면 접근 불가              | 분실시 Key 값 생성 코드 등을 사용하여 변경                   |
| DEBUG                    | True/False                                                   | 운영중일때 False로 변경                                      |
| ALLOWED_HOST             | 외부로부터 허용된 호스트 목록                                | DEBUG=True일 경우 웹 페이지 접근 가능<br />DEBUG=False일 경우 허용된 호스트만 접근 가능 |
| INSTALLED_APPS           | APP을 생성할 경우 추가해야 한다                              |                                                              |
| MIDDLEWARE               | 보안, 세션, 암호화 통신 시 사용                              |                                                              |
| ROOT_URLCONF             | 최상단의 URL설정 파일 지정                                   | url.py                                                       |
| TEMPLATES                | 프로젝트 및 앱의 웹페이지 양식 저장                          | 프로젝트 : /프로젝트명/templates/<br />앱 : /앱명/templates/ |
| WSGI_APPLICATION         | settings.py에서는 WSGI를 어디서 사용하는지 설정할 수 있고, <br />'프로젝트명'.wsgi.application 이라 함은 /프로젝트명/wsgi.py 파일의 application 부분을 WSGI_APPLICATION으로 사용한다는 것을 뜻함 | 변경 안함                                                    |
| DATABASE                 | DB 지정                                                      |                                                              |
| AUTH_PASSWORD_VALIDATORS | 사용자 비밀번호에 대한 유효성 관리                           |                                                              |
| LANGUAGE_CODE            | 기본 언어 지정                                               |                                                              |
| TIME_ZONE/USE_TZ         | 표준 시간대 설정<br />USE_TZ 는 Time Zone 사용 여부를 나타내는 것 (True)를 유지 | 한국 표준시 : Asia/Seoul                                     |
| USE_I18N/USE_L10N        | 국제화(I18N), 현지화(L10N) 지원여부 결정                     | 기본값(True) 유지                                            |
| STATIC_URL               | 정적파일 위치 지정                                           |                                                              |

* 추가 변수를 생성하여 관리할 수 있다

------

## manage.py

| 구분            | 설명                   | 비고                                                         |
| --------------- | ---------------------- | ------------------------------------------------------------ |
| runserver       | 웹 서버 작동           |                                                              |
| startapp        | Django 앱 생성         | 앱의 생성 및 삭제에 제한은 없다<br />생성 후 settings.py의 INSTALLED_APPS에 등록 해야 한다 |
| makemigrations  | DB 모델 생성           | Django 프로젝트에서 사용하는 모든 앱에서 DB 모델에 대한 변경사항이 있을 경우 이를 하나의 파일로 생성하는 작업 (migrations 디렉토리에 신규 파일이 생성됨) |
| migrate         | DB 모델 변경사항 적용  | Django 앱에서 DB 모델에 대한 변경사항을 적용할 때 사용       |
| inspectdb       | DB 모델 클래스 생성    | $ python manage.py inspectdb [테이블명]<br />Django에 연결된 DB모델의 테이블을 클래스(class) 형태로 가져오는 명령어<br />[테이블명]을 붙이지 않으면 모든 테이블을 가져온다<br />models.py에 클래스 형태로 기록하기 위해 '>'를 사용한다<br />$ python manage.py inspectdb boards > testapp/models.py |
| createsuperuser | 관리자 계정 생성       | 관리자 페이지 접속을 위한 사용자 생성                        |
| collectstatics  | 정적(static) 파일 배치 | 개발환경에서 /static/ 디렉토리에 관리하던 정적 파일을 <br />배포환경에서 Django 프로젝트의 루트(Root) 디렉토리로 정적 파일을 모두 배치시킬 때 사용하는 명령어<br />배포 환경에서는 개발 환경과 달리 정적파일을 사전에 배치하지 않으면 이들 파일을 적용할 수 없으므로 배포 이전에 사용해야 한다 |
| shell           | 파이썬 코드 수행       | Python shell과 동일하지만, 현재 사용중인 Django 웹 애플리케이션의 명령을 수행할 수 있는 환경 제공<br />기본적인 Python 명령어를 포함해서 Django에서 제공하는 패키지 및 모듈과 사용자가 정의한 패키지도 사용하여 코드를 개발하는 것과 동일하게 수행할 수 있다 |

