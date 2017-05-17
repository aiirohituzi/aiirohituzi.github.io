---
title: Django request.body 관련 메모
date: 2017-05-17 23:24:03
tags: django, request, serialize
---

### Django로 POST request 관련으로 간단한 api를 짜던 도중 문제가 발생


Postman이라는 프로그램으로 POST 요청을 하면 정상적으로 데이터가 받아지는데 반해

직접 만든 클라이언트측에서 axios를 통해 POST를 요청하면 QueryDict에 아무런 데이터도 받아지지 않는 현상이 일어났다.

한참을 헤맨 결과 request.POST가 아닌 request.body에 얻어지는 데이터를 직접 출력하여 원인을 발견했다.

```
Postman : 
b'----------------------------418318425319320142162885\r\nContent-Disposition: form-data;name="user"\r\n\r\n○○○○○\r\n----------------------------418318425319320142162885\r\nContent-Disposition: form-data; name="password"\r\n\r\n○○○○○○○○\r\n----------------------------418318425319320142162885--\r\n'

axios : 
b'{"user":"○○○○○","password":"○○○○○○○○"}'
```

Postman의 경우 기본적으로 여러가지 설정이 되어있어 바로 django에서 이를 해석하고

request.POST를 통해 얻어올 수 있지만 axios를 통해 보낸 경우 아무런 설정을 집어넣지 않은 채로

요청하였기 때문에 문제가 발생했다.

문제의 원인을 찾기가 힘들었을뿐이지 찾고나니 다행히 stackoverflow에서 손쉽게 해답을 얻을 수 있었다.


Django는 JSON 페이로드를 실제로 비 직렬화하지 않으니 직접 body 데이터를 비 직렬화해서 얻어야 한다.
```python
import json
...

json.loads(request.body)
```