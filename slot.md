# slot

먼저 기본 셋팅을 해주겠습니다.

```markup
<body>
    <div id="app">
       
    </div>
    <script>
        Vue.component('my-comp',{
            template:'<div> </div>',
        })
        const vm = new Vue({
            el:'#app',
        })
    </script>
</body>
```

이후에 div태그 안에 컴포넌트를 넣어준뒤 그 안에 텍스트를 넣어주었습니다.

```markup
    <div id="app">
       <my-comp>Hello Slot</my-comp>
    </div>
```

![&#xC544;&#xBB34;&#xAC83;&#xB3C4; &#xCD9C;&#xB825;&#xB418;&#xC9C0; &#xC54A;&#xC558;&#xC5B4;&#xC694;.](.gitbook/assets/image%20%2813%29.png)

{% hint style="warning" %}
컴포넌트가 렌더링될때는 컴포넌트사이에 특정 컨텐츠를 렌더링되지 않습니다.
{% endhint %}

컴포넌트에서 그 컨텐츠를 받아줄 slot을 사용해주겠습니다. 

```markup
<body>
    <div id="app">
       <my-comp>Hello Slot</my-comp>
    </div>
    <script>
        Vue.component('my-comp',{
            template:'<div><slot></slot></div>',
        })
        const vm = new Vue({
            el:'#app',
        })
    </script>
</body>
```

컴포넌트 안에 들어있는 내용을 slot태그로 받아주었습니다.

![&#xC798; &#xB098;&#xC624;&#xACE0; &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;.](.gitbook/assets/image%20%2831%29.png)

그럼 조금더 알아보겠습니다. 

slot안에 컨텐츠를 넣어보세요.



```text
Vue.component('my-comp',{
    template:'<div><slot>대체 콘텐츠</slot></div>',
})
```

하지만 아무것도 렌더링 되지는 않아요. 

그럼 이제 html안에서 컴포넌트 사이에 있는 컨텐츠를 지워주세요.

```text
    <div id="app">
       <my-comp>Hello Slot</my-comp>
    </div>
```

![&#xC798; &#xCD9C;&#xB825;&#xB418;&#xACE0; &#xC788;&#xC8E0;?](.gitbook/assets/image%20%288%29.png)

컴포넌트 안에 컨텐츠가 제공되고 있으면 그게 제공되지만 아무것도 없다면 slot안에 있는 것을 출력해줍니다. 

### slot이름

slot에 이름을 지정해 줄수도 있습니다.

```markup
<body>
    <div id="app">
       <my-comp>
           <div slot="slot1">Hello Slot!</div>
           <input type="text">
       </my-comp>
    </div>
    <script>
        Vue.component('my-comp',{
            template:'<div><slot name="slot1"></slot></div>',
        })
        const vm = new Vue({
            el:'#app',
        })
    </script>
</body>
```

이렇게 하면 div태그를 slot1에 렌더링할 내용으로 선택해준 것입니다. 

그럼 **Hello Slot!** 만 출력이 되겠죠!

만약 input도 추가를 해주려면 slot2를 만들어 지정해주던지, 아니면 이름없는 slot을 추가해주면 됩니다.

```markup
template:'<div> <slot></slot> <slot name="slot1"></slot> </div>',
```

여기서 중요한것은 slot이 앞에 있지만, 실제 컨텐츠 input은 뒤에 위치해 있습니다.

![&#xD558;&#xC9C0;&#xB9CC; slot&#xC774; &#xC9C0;&#xC815;&#xD55C; &#xC21C;&#xC11C;&#xB85C; &#xB80C;&#xB354;&#xB9C1; &#xB418;&#xC5C8;&#xC2B5;&#xB2C8;&#xB2E4;.](.gitbook/assets/image%20%2815%29.png)

### 범위를 가지는 slot

자식요소에 slot을 설정하고 데이터를 연결하고 그 데이터를 부모요소에서도 사용할 수 있도록 해줍니다. 

```markup
<body>
    <div id="app">
       <my-comp>
       </my-comp>
    </div>
    <script>
        Vue.component('my-comp',{
            template:'<div> <slot my-slot-data="Hello Slot!"></slot> </div>',
        })
        const vm = new Vue({
            el:'#app',
        })
    </script>
</body>
```

slot에 my-slot-data라는 커스텀 속성을 만들어 주었습니다. 

이걸 어떻게 사용할 수 있을까요? 

```markup
<body>
    <div id="app">
       <my-comp>
           <template slot-scope="myProps">
               {{myProps.mySlotData}}
           </template>
       </my-comp>
    </div>
    <script>
        Vue.component('my-comp',{
            template:'<div> <slot my-slot-data="Hello Slot!"></slot> </div>',
        })
        const vm = new Vue({
            el:'#app',
        })
    </script>
</body>
```

slot-scope를 사용하면 slot에 특정 데이터를 담아두었다가 부모요소에서 사용해 줄 수 있습니다. 

그렇다면 data도 연결해서 사용이 가능한지 한번 알아보겠습니다. 

```markup
Vue.component('my-comp',{
    template:'<div> <slot :my-slot-data="message"></slot> </div>',
    data(){
        return {message: "Hello Slot2!!"}
    }
})
```

message라는 데이터를 만들어 :my-slot-data로 바인딩 \(꼭 바인딩\) 해주었습니다. 

![](.gitbook/assets/image%20%2828%29.png)

```markup
    <div id="app">
       <my-comp>
           <template slot-scope="myProps">
               {{myProps.mySlotData}}
           </template>
       </my-comp>
    </div>
```

위 코드를 보면 slot에 정의된 데이터를 myProps라는 객체안에 받게되고 그 객체안에 저장된 slot데이터를 꺼내서 쓰는 것인데, 이경우에는 비구조화 할당을 해주면 되겠죠??

```markup
    <div id="app">
       <my-comp>
           <template slot-scope="{mySlotData}">
               {{mySlotData}}
           </template>
       </my-comp>
    </div>
```

위 처럼도 사용할 수 있습니다.

일반적으로 자주 사용되는 용법은 아니지만, 간혹 사용하는 경우가 생기니 개념적인 부분도 알고 있으면 도움이 될것입니다!!

