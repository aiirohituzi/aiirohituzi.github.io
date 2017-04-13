---
title: HTML5 - localStorage
date: 2017-04-13 20:53:45
tags: HTML5, localStorage
---
출처: [w3schools.com](https://www.w3schools.com/html/html5_webstorage.asp)

__Local Storage__ 란 __HTML5__ 부터 지원되는 데이터 저장공간이다.

### Cookie
+ 도메인당 4KB 가 최고용량

### LocalStorage
+ 2.5MB ~ 5MB 까지 저장 가능 (브라우저마다 최고용량이 다름)
+ 서버로 전송되지 않음.

## 사용 예시
```js
// Store
localStorage.setItem("lastname", "Smith");
// Retrieve
document.getElementById("result").innerHTML = localStorage.getItem("lastname");
```
setItem으로 값을 설정하고 getItem으로 가져온다.

```js
// Store
localStorage.lastname = "Smith";
// Retrieve
document.getElementById("result").innerHTML = localStorage.lastname;
```
위와같이 setItem 과 getItem 메소드를 꼭 사용하지 않아도 직접 값을 설정하고 가져올 수 있다.



localStorage의 특징은 텍스트형으로 밖에 저장을 할 수 없는 점이다.

객체를 저장하고자 한다면
JSON.stringify() 를 통해 text로 변환하여 저장해야 한다.
```js
let object = { text: 'test'};
localStorage.dataName = JSON.stringify(object);
```

저장된 객체(텍스트로 변환 된)를 불러오려면
JSON.parse() 를 통해 다시 객체로 변환하면 된다.
```js
JSON.parse(localStorage.dataName);
```

localStorage를 초기화 하고자 한다면 아래의 메소드를 사용하면 된다.
```js
localStorage.clear();
```