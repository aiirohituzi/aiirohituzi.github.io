---
title: 윈도우에서 Apache로 django구동 관련 메모
date: 2019-01-22 22:10:39
tags: django
---

[정보 출처]
[Windows에서 Apache2.4 + mod_wsgi 설치](https://dgkim5360.tistory.com/entry/install-apache24-mod-wsgi-for-windows)
[django 공식 문서의 mod_wsgi 설정관련](https://docs.djangoproject.com/en/2.1/howto/deployment/wsgi/modwsgi/)


## mod_wsgi 설치

Apache 서버에서 Python 기반의 웹 어플리케이션(django)를 가동하려면 **mod_wsgi**이라는 플러그인을 설치해야 한다.


mod_wsgi 플러그인은 **윈도우 32bit 버젼**만을 지원한다.

현재 기준으로 릴리즈 사이트의 코멘트를 확인해보면 윈도우에서 사용가능한 최신 버젼은 **4.4.12 버젼**



apache 서버 설치 후(원글 내용대로 따라한다면 2.4버젼) 내려받은 mod_wsgi 파일의 압축을 풀면 나오는 파일 중

Apache24-win32-VC9 폴더 안에 있는 mod_wsgi-py27-VC9.so 파일을 Apache24/modules 폴더에 복사 후

이름을 간단하게 mod_wsgi.so로 변경

플러그인을 불러오도록 설정파일(httpd.conf)에
```
#httpd.conf

LoadModule wsgi_module modules/mod_wsgi.so
```
라고 한 줄 추가하면 설치 완료
<br><br>


## mod_wsgi 관련 설정
```
#httpd.conf

WSGIScriptAlias / /path/to/mysite.com/mysite/wsgi.py
WSGIPythonHome /path/to/venv
WSGIPythonPath /path/to/mysite.com

<Directory /path/to/mysite.com/mysite>
    <Files wsgi.py>
        Require all granted
    </Files>
</Directory>
```

django 프로젝트 디렉토리를 살펴보면 settings.py 파일이 있는 디렉토리에 wsgi.py파일이 있는것을 확인할 수 있다.
WSGIScriptAlias / "이부분" 에 해당 파일의 경로를 파일명과 함께 입력하면 된다.

WSGIPythonHome 에는 python 가상환경의 경로를 입력

WSGIPythonPath 에는 django 프로젝트의 manage.py 파일이 위치해 있는 루트 디렉토리의 경로를 입력하면 된다.

<Directory "wsgi.py파일이 위치한 경로"> 이곳에 입력해야할 경로는 말 그대로 wsgi.py파일이 위치해있는 경로

즉, WSGIScriptAlias 에 입력했던 경로에서 파일명인 wsgi.py만 빼면 된다.


해당 설정을 마치고 아파치 서버를 재기동 시키면 아파치 서버를 통해 django 서버에 접속되는 모습을 확인할 수 있다.
