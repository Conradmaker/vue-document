# props 와 데이터전달

```markup
<body>
    <div id="app">
        <my-comp :msg="message"/>
    </div>
    <script>
        Vue.component('my-comp',{
            template:'<div>{{msg}}</div>',
            props:['msg']
        })
        const vm = new Vue({
            el:'#app',
            data(){
                return{
                    message:'Hello'
                }
            }
        })
    </script>
</body>
```

my-comp라는 컴포넌트를 만들어주고, props즉 속성msg를 만들어준뒤, app의 message데이터를 msg로 바인딩 해주었습니다.

props: 에 배열의 형식으로 사용할 props를 정의 해주었는데, msg가 가지고 있는 기본적인 옵션을 설정해 줄 수 없습니다. 

그렇기 위해서는 배열데이터를 객체데이터로 바꿔주면 됩니다. 

일단 단순하게 msg데이터는 문자데이터라는 것을 정의해 줄까요?

### 데이터타입 설정

```markup
Vue.component('my-comp',{
     template:'<div>{{msg}}</div>',
     props:{
           msg:{type:String}   //문자데이터만
     }
})
```

흡사 타입스크립트?? 이렇게 되면 문자열을 제외한 데이터타입은 들어올 수가 없습니다. 

### 기본값 설정

이번에는 기본값을 설정해 보아요 .

```markup
Vue.component('my-comp',{
     template:'<div>{{msg}}</div>',
     props:{
          msg:{
           type:String   //문자데이터만
           default:'Default!!'  //만약 msg가 없다면 Default!!출력
           }
     }
})
```

### 타입 중복

배열로 타입부분을 정의해주면 여러데이터를 허용해 줄 수도 있습니다.

```markup
Vue.component('my-comp',{
     template:'<div>{{msg}}</div>',
     props:{
          msg:{
           type:[String,Number],   //문자데이터만
           default:'Default!!'  //만약 msg가 없다면 Default!!출력
           }
     }
})
```

### 필수props설정

required 를 통해 props가 없다면 에러를 출력할 수도 있습니다. 

```markup
Vue.component('my-comp',{
     template:'<div>{{msg}}</div>',
     props:{
          msg:{
           type:[String,Number],   //문자데이터만
           required:true  //필수
           }
     }
})
```

만약 필수옵션이 설정되었다면 필수로 데이터가 들어와야 하기 때문에, default는 없어도 되겠죠?? 

### 유효성검증

validator는 기본적으로 함수입니다. 또한 매게변수로는 msg가 받은 특정한 값 즉, 'Hello'가 들어갈 수 있습니다.

```markup
Vue.component('my-comp',{
     template:'<div>{{msg}}</div>',
     props:{
          msg:{
           type:[String,Number],   //문자데이터만
           required:true  //필수,
           validator: function(value){
                    return value === 'Hello';
                }
           }
     }
})
```

validator함수안에 true가 return되야만, 유효성검사에 통과하게 됩니다. 

위의 경우에는 `"!"` 가 빠져있기 때문에 에러메시지가 출력됩니다.

