---
title: javascript로 json 오브젝트 sort
date: 2017-11-12 21:38:42
tags: javascript
---

Array.prototype.sort() 라는 함수를 사용하여 json 오브젝트를 정렬 가능

기본 정렬 순서는 문자열 유니 코드 코드 포인트에 따른다.

```js
arr.sort()
arr.sort(비교 함수)
```
사용시엔 위와 같은 방식으로 사용 (json은 javascript에서 배열처럼 취급하기 때문에 array의 내장 함수로 정렬)

<br></br>

예시 코드
```js
this.r_ratings.sort(function (a,b){
    return(a.USER.toLowerCase() < b.USER.toLowerCase()) ? -1 : (a.USER.toLowerCase() > b.USER.toLowerCase()) ? 1 : 0
})
```

개발중에 사용했던 코드를 예시로 들면

평가 함수에 사용되는 매개변수인 a, b는 각 현재 행, 다음 행을 뜻한다.

return값에 따라 정렬을 위해 취할 동작이 결정 되는데 각 각
__0 : 아무 동작도 하지 않음
1 : 현재 행을 다음 행보다 아래로 정렬
-1 : 현재 행을 다음 행보다 위로 정렬__
와 같은 정렬 작업을 수행한다.

에시 코드에선 각 행의 USER라는 값을 전부 소문자로 통일하여 오름차순으로 정렬되도록 비교식을 넣은 모습이다.