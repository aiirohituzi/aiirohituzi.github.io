---
title: React.js Component Lifecycle API
date: 2017-04-13 19:57:51
tags: React.js, Lifecycle
---

출처 : [inflearn - VELOPERT의 React.js 강좌](https://velopert.com/1130)

![Component Lifecycle API](https://www.inflearn.com/wp-content/uploads/Screenshot-from-2016-12-10-00-21-26-1.png)

## constructor
```js
constructor(props) {
    super(props);
    console.log("constructor");
}
```
컴포넌트 첫 생성 시 실행
기본 state 를 설정 할 수 있다


## componentWillMount
```js
componentWillMount() {
    console.log("componentWillMount");
}
```
컴포넌트가 DOM 위에 만들어지기 전에 실행
그래서 여기에선 DOM 처리가 불가능


## componentDidMount
```js
componentDidMount() {
    console.log("componentDidMount");
}
```
첫 렌더링 마친 후 실행
이 안에서 다른 자바스크립트 프레임워크 연동 및 setTimeout, setInterval 및 AJAX 사용
DOM 처리 가능


## componentWillReceiveProps
```js
componentWillReceiveProps(nextProps) {
    console.log("componentWillReceiveProps: " + JSON.stringify(nextProps));
}
```
props를 받을 때 실행
props에 따라 state를 업데이트 할 때 사용하면 유용
내부에서 setState 사용 가능
아직 props를 받지 않은 상태이므로 미리 받을 props를 nextProps를 통해 접근


## shouldComponentUpdate
```js
shouldComponentUpdate(nextProps, nextStage) {
    console.log("shouldComponentUpdate: " + JSON.stringify(nextProps)) + " " + JSON. stringify(nextState);
    return true;
}
```
props/state 병경 시 리렌더링 여부를 결정
실제 사용 시 필요한 비교를 하고 값을 반환해야 한다
(ex: return nextProps.id !== this.props.id)
JSON.stringify 를 사용하여 여러 field를 편하게 비교


## componentWillUpdate
```js
componentWillUpdate(nextProps, nextState) {
    console.log("componentWillUpdate: " + JSON.stringify(nextProps) + " " + JSON.stringify(nextState));
}
```
컴포넌트 업데이트 전 실행
여기서 절대로 setState를 사용하지 말 것


## componentDidUpdate
```js
componentDidUpdate(prevProps, prevState) {
    console.log("componentDidUpdate: " + JSON.stringify(prevProps) + " " + JSON.stringify(prevState));
}
```
컴포넌트가 리렌더링을 마친 후 실행
여기서도 setState 사용 금지
props/state 가 변경 된 후이므로 변경 이전의 값에 접근하려면 prevProps/prevState 를 통해 접근


## componentWillUnmount
```js
componentWillUnmount() {
    console.log("componentWillUnmount");
}
```
컴포넌트가 DOM 에서 사라진 후 실행