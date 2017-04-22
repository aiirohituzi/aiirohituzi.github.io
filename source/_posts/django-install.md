---
title: django 설치방법
date: 2017-04-22 22:35:30
tags: python, django
---

먼저 __*virtualenv*__ 를 설치 후 가상환경으로 들어간다.
([가상환경 설치방법](https://aiirohituzi.github.io/2017/04/10/python-virtualenv/))

pip 를 따로 설치하지 않았어도 python 가상환경 내에 구성되어있기 때문에 pip를 이용하여 손쉽게 django를 설치할 수 있다.

* 설치 명령어
```
$ pip install django
    최신버젼으로 알아서 설치한다.
$ pip install django==x.x
    따로 원하는 버젼을 지정하여 설치할 수 도 있다.
```

* 프로젝트 생성
```
$ django-admin startproject 프로젝트명

프로젝트명/
├── manage.py
└── pystagram
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py

위와 같은 구조로 파일이 생성된다.
```

* 앱 생성
django에서는 프로젝트 내부의 각각의 기능들을 앱별로 나누어서 관리한다.
```
$ python manage.py startapp 앱명칭
```

### 그 외 기본적인 django 관련 명령어
* 개발용 웹서버 실행
```
$ python manage.py runserver
    전달인자가 없을 경우 호스트는 127.0.0.1, 포트는 8000을 사용
$ python manage.py runserver 127.0.0.1:8080
    바꾸고 싶다면 따로 지정하여 명령할 수 있다.
```
서버가 성공적으로 실행됐다면 브라우저의 url에 127.0.0.1:8000 혹은
localhost:8000 을 입력하여 접근할 수 있다.

* 데이터베이스 동기화
django framework 에서 제공하는 도구가 사용하는 데이터베이스 관련작업을 자동으로 진행
```
$ python manage.py migrate
```

* 최고 권한 이용자 생성
```
$ python manage.py createsuperuser
Username (leave blank to use '*****'): admin
Email address: 
Password:
Password (again):
Superuser created successfully.
```

* 사용자의 비밀번호 변경
```
$ python manage.py changepassword admin
```