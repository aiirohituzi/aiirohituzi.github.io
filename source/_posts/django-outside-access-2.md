---
title: django media 파일
date: 2019-01-25 21:00:10
tags: django
---

* 이전 관련 글
[django 프로젝트 외부 디렉토리 접근방법](https://aiirohituzi.github.io/2017/07/12/django-outside-access/)

* 참고 자료 출처
[Handling Media Files in Django](https://overiq.com/django-1-10/handling-media-files-in-django/)
[Django 정적 파일 기능 이해하기](https://blog.hannal.com/2015/04/start_with_django_webframework_06/)




이전에 클라이언트로부터 업로드된 이미지에 접근할 수 있는 방법을 찾지 못해 정말 단순무식하게 클라이언트서버측 폴더에

파일을 업로드 시켜서 해결했었던 적이 있다.

개발 서버에서 작업할 때는 위와 같이 해결해도 전혀 문제가 되지 않았지만 실질적으로 외부접속을 테스트하려고

막상 웹서버에 올리려고 하니 당연하게도 문제가 발생할 수 밖에 없었다.

상대경로를 이용하여 클라이언트측 디렉토리에 접근하여 업로드하는 방식이니 서로 다른 서버에 올라가있는 상태로는

정상적으로 동작할 수가 없는게 당연하기 때문<br><br>



결국 다시 방법을 찾은결과 django 에서 이를 위한 media 파일을 지원하고 있다는걸 알 수 있었다.

static 파일처럼 media 파일도 정적 파일이긴 하지만 media 파일은 웹에서 업로드된 파일로

언제 어떤 파일이 정적 파일로 제공되고 준비되는지 예측할 수 없다는 점이 다르다.<br><br>



이 방식을 사용함으로 인해 처음 원하던대로 django 서버에서 db와 image파일들을 관리하고 프론트엔드 서버에서

접근하는 구조를 이제서야 완성할 수 있었다.<br><br>





## 설정 방법

settings.py 파일에 다음과 같이 media 파일들이 들어갈 실제 경로와 URL을 설정해준다.
```py
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
MEDIA_URL = '/media/'
```

그리고 urls.py 파일에 url 패턴을 추가해줘야 한다.
```py
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    url(r'^admin/', admin.site.urls),
    ...
    ...
    ...
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

이제 지정한 media 디렉토리 내에 아무거나 이미지파일을 넣어보고

`http://서버주소/media/이미지파일명` 경로를 입력하여 들어가면 해당 이미지를 확인할 수 있을것이다.



<br><br><br><br>
여기서 이전에 사용했던 파일 업로드 코드에서 업로드 될 경로만 media 디렉토리로 지정해주어

원하던 백엔드서버로써의 기능을 수행하는 django 서버의 모습을 만들어주었다.