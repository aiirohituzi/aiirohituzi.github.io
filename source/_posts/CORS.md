---
title: CORS 관련 메모
date: 2017-04-29 22:30:43
tags: CORS, Cross Origin Resource Sharing
---

## CORS 란?
**Cross Origin Resource Sharing** 의 준말
서로 다른 도메인 간 리소스가 요청될 시 (cross-domain) 동일 출처 정책 (Same-Origin Policy) 에 관련하여 보안 문제로 간주하고 이를 브라우저에서 차단한다.
CORS를 활성화시키면 CORS는 웹 서버에게 보안 cross-domain 데이터 전송을 활성화하는 cross-domain 접근 제어권을 부여한다.

## django project 개발 서버에서의 CORS 설정
django-cors-header 모듈을 사용하면 간단하게 해결 가능

* pip를 사용하여 모듈을 설치
```
$ pip install django-cors-headers
```

* setting.py 에 모듈 추가 및 각종 설정
```python
INSTALLED_APPS = (
    ...
    'corsheaders',
)

MIDDLEWARE_CLASSES = (
    'corsheaders.middleware.CorsMiddleware',
    'django.middleware.common.CommonMiddleware',
    ...
)
# CorsMiddleware가 django의 CommonMiddleware 위로 와야 한다.


CORS_ORIGIN_ALLOW_ALL = False

CORS_ORIGIN_WHITELIST = (
    '<YOUR_DOMAIN>[:PORT]',
)
# 위와 같이 설정하여 하나의 도메인만 서버와 통신할 수 있도록 허용할 수도 있다.
# 모두 허용하고 싶다면 whitelist를 작성하지 않고 CORS_ORIGIN_ALLOW_ALL의 값을 True로 설정
```