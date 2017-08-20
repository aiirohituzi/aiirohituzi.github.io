---
title: react-bootstrap 사용 시 style 덮어쓰는 방법
date: 2017-08-20 22:19:07
tags: react-bootstrap
---

react 환경에서 bootstrap을 사용하기 위해 npm으로 react-bootstrap을 설치하여 사용하는 도중 사이즈나 정렬방식, 간격 등을 원하는대로 재설정할 필요가 생겼다.

기본적으로 bootstrap에 정의된 css를 따라가기에 style을 직접 덮어씌워야 변경이 가능한데

stack overflow 를 통해 그 방법을 찾을 수 있었다.



```js
<InputGroup.Addon style={{
    width: '20%',
    paddingTop: '0',
    paddingRight: '0',
    paddingBottom: '0',
    paddingLeft: '0',
}}>

<FormControl componentClass="select" placeholder="select" style={{width: '100%'}}>

<p style={{textAlign:"right"}}>
```


위의 코드와 같이 __\{ \{  \} \}__ 로 감싸서 style props에 값을 넘기는 느낌이다.

각 항목의 명칭들이 언뜻 실제 css를 정의하는것과 비슷해보이지만 text-align 같은 속성들은

가운데의 -를 지우고 단어를 대문자로 구분하여 textAlign으로 입력해주어야 한다.

또한 각 값을 구분할때 세미콜론(__;__)이 아닌 반점(__,__)으로 구분해주어야 하며 문자열방식으로 입력해주어야 한다.