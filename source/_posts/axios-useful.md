---
title: axios 사용 관련 메모
date: 2017-06-14 18:26:49
tags: axios
---
참고 자료 출처 : [npm axios](https://www.npmjs.com/package/axios#example)

공식 문서를 보면 가장 기본적인 사용 예시로 다음과 같은 방법이 소개되어있다.
```js
// Make a request for a user with a given ID 
axios.get('/user?ID=12345')
.then(function (response) {
    console.log(response);
})
.catch(function (error) {
    console.log(error);
});
 

// Optionally the request above could also be done as 
axios.get('/user', {
    params: {
        ID: 12345
    }
})
.then(function (response) {
    console.log(response);
})
.catch(function (error) {
    console.log(error);
});


axios.post('/user', {
    firstName: 'Fred',
    lastName: 'Flintstone'
})
.then(function (response) {
    console.log(response);
})
.catch(function (error) {
    console.log(error);
});
```

아무것도 모른 상태로 처음 시도해볼 때는 이정도의 사용법으로도 문제가 없었으나

좀더 깊이 들어갈수록 당연스럽게 여러가지 문제에 부딪히게 되었다.

아무런 설정도 없이 파라메터와 메소드 방식만 담아서 요청을 하니 요청을 받는 프로그램 측에서

당연히 이를 제대로 해석하지 못해 문제가 된 것.<br></br>



임시방편으로 해결책을 찾아 급한 불은 껐지만 나중에 보니 서버측에서 말그대로 데이터만 받고

양식을 다시 짜올리는 비효율적인 방법을 사용하고있었다.<br></br>



아이러니하게도 이미지파일 정보를 전송하는 방법을 찾던 도중 보다 확실한 방법을 찾게되었다.

덕분에 코드를 관리하기에도 좀더 용이해졌는데 파라메터가 담긴 폼객체와 설정정보가 담긴 객체를 따로

미리 만들어 axios 요청 메소드에 통째로 포함시키는 방법이 있었다.

```js
var data = new FormData();      //  먼저 FormData 객체를 생성

...

data.append('user', loginId);
data.append('password', loginPw);
data.append('title', title);
data.append('content', content);
data.append('image', image);        // 순서와 관계없이 원하는 파라메터를 집어넣는다.

// 관련 설정 값을 묶어서 변수로 전달
const config = {
    headers: { 'content-type': 'multipart/form-data' }
}

// axios 요청 메소드에 파라메터로 전달
axios.post('url', data, config)
.then(function (response) {
    console.log(response);
})
.catch(function (error) {
    console.log(error);
});
```

위와 같은 방식을 취함으로써 가독성도 향상되었을뿐더러 코드 관리도 편해졌고

요청 데이터가 확실한 양식을 갖추어 서버측에서 이를 받았을 시 처리하기도 용이해지는 효과를 얻을 수 있었다.