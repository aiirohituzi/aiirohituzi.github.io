---
title: django csrf 관련 메모
date: 2017-08-04 22:54:33
tags: django, csrf
---

[CSRF 공격 관련 상세 설명글 링크](http://www.insilicogen.com/blog/55)

[django 공식 문서의 CSRF 관련 항목](https://docs.djangoproject.com/en/1.11/ref/csrf/)

<br>

그동안 그냥 ajax 요청이 잘 수행되도록 views의 함수앞에 넣었던 데코레이터인

__@csrf_exempt__ 는

django의 미들웨어가 CSRF 공격으로부터 보호해주는 기능을 적용하지 않도록 하는 데코레이터라는듯 하다.

<br>

django는 ajax로 post 요청이 날아왔을때 request.POST 내의 CSRF token이 CSRF cookie와 일치하는치 체크한다.

내가 사용한 방법은 외부의 다른 서버로부터 요청을 보냈기 때문에 이를 확인하지 않도록 @csrf_exempt 데코레이터를 넣어

일단 작업이 수행되도록 한 것.