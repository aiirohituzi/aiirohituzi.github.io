---
title: django에서 데이터베이스에 Insert하기
date: 2017-06-20 22:38:08
tags: django
---

클라이언트로부터 파라메터를 입력받아 request 가 날아오면

그 데이터들을 이용하여 따로 query 를 짤 필요 없이 django 내장 함수들을 통해 처리할 수 있는

방법이 있다. (이 방법이 더 쉬운지에 대해서는 개인차에 따라 다르니 본인이 좋다고 생각하는 방법을 사용하면 될듯)<br></br>


간단한 예시를 들어 설명하자면

```py
postForm = PostForm(request.POST)
```

request 를 받을 함수 내에서 request 데이터를 받아 해당 model 의 Form 객체를 생성한다.

이 때 request 로 넘어오는 파라메터 값의 명칭이 Form에 정의해놓은 명칭과 일치해야 자동으로 값을 입력한다.<br></br>


```py
if postForm.is_valid():
    post_obj = postForm.save(commit=False)      # true일 경우 바로 데이터베이스에 적용, 현재 유저정보가 담기지 않았기에 not null 제약조건에 걸려 작업이 실패하므로 false
    post_obj.owner_id = user_row.id
    post_obj.save()                             # obj.save(commit=True) 와 동일
```

그 후 Form.save() 라는 함수를 이용하여 DB에 바로 Insert 를 해줄 수 있다.

인자로 commit 이란 것을 설정해줄 수 있는데, True 로 설정해놓았다면 그 즉시 Insert 작업을 시행하고

False 라면 DB 에 넣을 준비가 되어있는 객체를 생성하여 받아올 수 있게된다.<br></br>

위의 예시의 경우 request 로 받지 않은 별도의 column 값을 입력하지 않아 Insert 에러가 발생하기 때문에

따로 입력작업을 한번 더 거친 후,

obj.save(commit=True) 함수를 통해 Insert 작업을 처리하는 모습이다.