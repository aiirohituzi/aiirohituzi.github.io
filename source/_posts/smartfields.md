---
title: smartfields
date: 2017-07-09 22:22:15
tags: django
---

django 서버에서 이미지 등 파일을 관리할 때 유용

내장모듈인 django.db의 models의 field대신

smartfields를 이용하면 데이터베이스에서 해당 레코드가 지워졌을 때

연결된 파일을 일일히 추적해서 삭제할 필요없이 알아서 삭제해준다.
</br>

### 이미지 필드 사용 예시
```py
# models
image = models.ImageField(upload_to='%Y/%m/%d/orig')

# smartfields
image = fields.ImageField(upload_to='%Y/%m/%d/orig')
```

지원되는 필드 타입도 기존에 존재하는 것이 대부분 지원되는 편이고

사용방법도 거의 동일한 느낌