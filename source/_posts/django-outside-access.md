---
title: django 프로젝트 외부 디렉토리 접근방법
date: 2017-07-12 23:46:05
tags: django
---

Server와 Client 모두 django로 제작한다면 이 방식을 사용할 일이 없다시피 하겠지만

Client측에서 Server쪽의 파일을 직접 접근해야할 필요가 생겨 해결법을 찾을 수 밖에 없었다.
<br/>

### settings.py
```py
...

# Build paths inside the project like this: os.path.join(BASE_DIR, ...)
BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))

...
```

settings에 기본적으로 root역할을 할 base 디렉토리 경로가 설정이 되어있는데

그것을 기준으로 바깥쪽의 경로에 접근할 수 있도록 설정할 수 있다.

```py
...

# Build paths inside the project like this: os.path.join(BASE_DIR, ...)
BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
FILES_DIR = os.path.abspath(os.path.join(BASE_DIR, '../../client/image/'))

...
```

위와 같이 한줄의 코드를 추가해주고 views.py에서 다음과 같이 접근할 수 있다.
<by/><by/>

### views.py
```py
from django.conf import settings
import os

...

file_path = os.path.join(settings.FILES_DIR, 'test_image.png')
image_data = open(file_path, "rb").read()
```

image파일뿐만 아니라 다른 형식의 파일도 접근 가능하다.
<br/><br/>


## model을 통한 외부 upload

위의 방법은 읽기는 가능하지만 model을 통해 업로드를 시도했을 경우 참조한 경로가

프로젝트의 외부에 존재한다는 오류와 함께 업로드에 실패하게 된다.

따라서 성공적으로 업로드를 하기 위해서는 다음과 같은 방법을 사용할 수 있다.

```py
from django.conf import settings
import os
from django.core.files.storage import FileSystemStorage

...

class Images(models.Model):
    fs = FileSystemStorage(location=settings.FILES_DIR)
    image = models.ImageField(upload_to='%Y/%m/%d/orig', storage=fs)

...
```

upload_to 에 입력할 경로에 settings.FILES_DIR + ' ... ' 같은 방법으로

입력하는 것이 아니라 FileSystemStroage 를 사용하여 위와같이 경로를 입력해주면

settings.FILES_DIR 경로(settings.py에서 지정해준 외부 디렉토리 경로)의

하위 경로에 upload_to의 경로대로 파일을 저장하게 된다.

<br/>
~~사족으로 smartfields의 database에서 레코드 제거시 연결된 파일을 추적하여 자동으로 삭제해주는 기능은 이 방식을 사용한경우 작동하지 않는 듯 하다...~~





* 2019-01-25 추가
django 내에서만 업로드된 이미지 파일을 다루는 방법
[django media 파일](https://aiirohituzi.github.io/2019/01/25/django-outside-access-2/)