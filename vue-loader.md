# Vue Loader

{% embed url="https://vue-loader-v14.vuejs.org/kr/" %}

지금까지 예제를들 통해 컴포넌트들을 많이 만들었는데, 문자열로 template를 입력하니, 많은 어려움이 있었습니다. 

vue에서는 컴포넌트들을 파일단위로 관리할 수 있게 해주는 Vue Loader를 제공하고 있습니다. 

Vue Loader란?

아래를 보면 template / script / style태그들이 있는데, 이걸 묶어서 하나의 컴포넌트로 만들어 줍니다.

![](.gitbook/assets/image%20%2840%29.png)

> 컴포넌트로 만들어주는 역할은 웹팩의 모듈인 vue-loader가 해주게 됩니다.

### Vue 컴포넌트 스펙

`*.vue` 파일은 HTML과 같은 문법을 사용하여 Vue 컴포넌트를 작성합니다. 각각의 `*.vue` 파일은 3가지 유형의 최상위 language block인 `<template>`, `<script>`와 `<style>`로 이루어집니다.



### Language Blocks

**&lt;template&gt;**

* 기본 언어 : `html`.
* 각 `*.vue` 파일은 한번에 최대 하나의 `<template>` 블록을 포함할 수 있습니다.
* 내용은 문자열로 추출되어 컴파일 된 Vue 컴포넌트의 `template` 옵션으로 사용합니다.

**&lt;script&gt;**

* 기본 언어 : `js` \(ES2015는`babel-loader` 또는`bubble-loader`가 감지되면 자동으로 지원됩니다\).
* 각 `*.vue` 파일은 한번에 최대 하나의 `<script>` 블록을 포함할 수 있습니다.
* 스크립트는 CommonJS와 같은 \(webpack을 통해 번들된 일반적인 `.js` 모듈같은\)환경 에서 실행됩니다. 다른 의존성을 `require()`할 수 있습니다. 또한 ES2015를 지원하여 `import`와 `export`를 사용할 수 있습니다.
* 스크립트는 Vue.js 컴포넌트 옵션 객체를 내보내야합니다. `Vue.extend()`에 의해 생성된 확장 생성자를 export하는 것도 지원되지만 평범한 객체를 추천합니다.

**&lt;style&gt;**

* 기본 언어 : `css`.
* 한개의 `*.vue`에서 여러개의 `<style>`태그를 지원합니다.
* `<style>`태그는 `scoped` 또는 `module` 속성을 가질 수 있습니다. \([Scoped CSS](https://vue-loader-v14.vuejs.org/kr/features/scoped-css.html)와 [CSS Modules](https://vue-loader-v14.vuejs.org/kr/features/css-modules.html)를 확인하세요\) 현재 컴포넌트에 스타일을 캡슐화 하는데 도움을 줍니다. 캡슐화 모드는 다른 여러개의 `<style>` 태그를 동일한 컴포넌트에 사용할 수 있습니다.
* 기본적으로, 내용이 추출되어 `style-loader`를 사용해 실제로 `<style>` 태그로 문서의 `<head>`에 동적으로 삽입됩니다. [모든 컴포넌트의 모든 스타일이 하나의 CSS 파일로 추출되도록 webpack을 설정](https://vue-loader-v14.vuejs.org/kr/configurations/extract-css.html)할 수 있습니다. -

### Webpack

[webpack](https://github.com/webpack/webpack)은 웹팩\(Webpack\)의 핵심 패키지이며,  
 [webpack-cli](https://github.com/webpack/webpack-cli)는 터미널에서 웹팩 명령\(Commands\)를 실행할 수 있게 해주는 도구입니다.

```text
$ npm i -D webpack webpack-cli
```

개발용으로 실시간 Reload 서버를 실행하기 위해 [webpack-dev-server](https://github.com/webpack/webpack-dev-server)를 설치합니다.

```text
$ npm i -D webpack-dev-server
```

[webpack-merge](https://github.com/survivejs/webpack-merge)는 웹팩 Config 객체를 병합\(merge\)하기 위해 설치합니다.  
 웹팩을 개발용\(`dev`\)과 배포용\(`build`\)으로 구분해 실행할 수 있습니다.

```text
$ npm i -D webpack-merge
```

`webpack.config.js` 파일을 생성합니다.  
 자세한 설정 내용은 [완성된 파일\(webpack.config.js\)](https://github.com/HeropCode/Vue-Todo-app/blob/master/webpack.config.js)을 참고하세요.



Vue loader설치

{% embed url="https://vue-loader.vuejs.org/guide/\#vue-cli" %}

```text
npm install -D vue-loader vue-template-compiler
```



그리고 root 디렉토리에 웹팩설정파일 webpack.config.js를 만들어 주세요.

```javascript
const path = require("path");
module.exports = {
  //진입점 (가장먼저 실행될 파일)
  entry: {
    app: path.join(__dirname, "main.js"), //app은 별칭
  },
  //결과물에 대한 설정
  output: {
    filename: "[name].js", //app.js [name] = 진입파일 별칭
    path: path.join(__dirname, "dist"),
  },
  //module,plugins는 처리과정에 들어감
  module: {
    rules: [
      {
        test: /\.vue$/, //vue라는 확장자를 찾으면
        loader: "vue-loader", //vue로더를 통해 해석한다.
      },
    ],
  },
  plugins: [new VueLoaderPlugin()], //추가적인 과정
};

```

