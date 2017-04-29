---
title: Webpack 개발서버에서 async/await 사용하기
date: 2017-04-30 02:25:12
tags: webpack, babel, async, await
---

참고 자료 출처:
[webpack](https://webpack.js.org/guides/code-splitting-async/#usage-with-babel-and-async-await)
[VELOPERT.LOG](https://velopert.com/2597)

Node.js에서 ES6를 완전히 지원하지 않는 문제로 webpack 개발서버를 실행하는 중 async 관련 syntax 오류로 컴파일하지 못하는 문제가 발생했다.

열심히 자료들을 찾아본 결과 Babel을 이용하면 해결할 수 있다는 것을 알게 되었다.

이미 babel-preset을 적용하여 사용하고 있지만

추가로 아래의 4가지 plugin 설정을 필요로 하는 상황이라 오류가 발생하고 있었다.
transform-async-to-generator
transform-class-properties
transform-regenerator
transform-runtime

다음과 같은 방법으로 plugin을 설치 및 webpack 설정을 함으로 문제를 해결했다.

* plugin 설치
기본적으로 이미 webpack과 babel-core, babel-loader, babel-preset-es2015 은 설정되어있다고 가정
```
$ npm install --save-dev babel-plugin-transform-async-to-generator babel-plugin-transform-class-properties babel-plugin-transform-regenerator babel-plugin-transform-runtime
```

* webpack.config.js 수정
```js
module.exports = {
  ...
  module: {
    rules: [{
      test: /\.js$/,
      exclude: /(node_modules)/,
      use: [{
        loader: 'babel-loader',
        options: {
          presets: [['es2015', {modules: false}]],
          plugins: [
            'transform-async-to-generator',
            'transform-class-properties',
            'transform-regenerator',
            'transform-runtime'
          ]
        }
      }]
    }]
  }
};
```