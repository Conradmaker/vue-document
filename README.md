# Hello VUE!!

vue.js 는 JS를 조금더 쉽게 사용하기 위한 도구입니다. 

아무리 쉽더라도 HTML / CSS / JS중급이상의 실력을 기르고 vue.js를 시작하기를 권장드려요 . 



또한 Node.js의 환경을 만들어주고 이용하기 때문에, 기본적인 npm의 지식정도는 다룰줄 아는 상태로 공부하시기를 권장드립니다 . 

vue.js는 또한 webpack환경에서 구동되기 때문에 webpack도 함께 공부하면 도움이 될 것입니다. 

Vue.js는 한글 공식문서가 아주 잘 정리되어 있기 때문에, 학습요건이 매우 좋은 편인데, React 나 Angular에 비해 상당히 쉬운 난이도를 가지고 있기 때문에, vue.js를 공부하는 것이 아주 좋은 선택이라고 생각됩니다. 

{% embed url="https://kr.vuejs.org/index.html" %}



vue를 불러오는 방법은 2가지가 있습니다.  

1. CDN
2. 다운로드

cdn으로 사용하는 방법을 알아볼 것인데, 그냥 아래코드를 ㄴhtml안에 넣어주기만 하면 됩니다.  

```text
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

그 뒤에 id가 app인 div태그와 그 안에 script태그를 만들어주세요.

```markup
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue test</title>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>
<body>
    <div id="app">
        <script>
           
           
        </script>
    </div>
</body>
</html>
```

이제 vue를 사용해 줄 것입니다 .

new Vue\(\)를 통해 새로운 뷰인스턴스를 사용하는데, 아래와 같이 사용하면 됩니다. 

```markup
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue test</title>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>
<body>
    <div id="app">
        {{msg}}
        <script>
            new Vue({
                el:'#app',
                data:{
                    msg:'Hello Vue!!'
                }
            })
        </script>
    </div>
</body>
</html>
```

el은 html element를 선택하는 선택자를 입력해주면 됩니다. 

data는 element에서 사용할 데이터를 지정해줄 수 있습니다. 

{{ }}안에 그 데이터의 key를 넣어주면 사용할 수 있습니다. 

![&#xB05D;!!](.gitbook/assets/image%20%2820%29.png)

