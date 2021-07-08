# Vue 인스턴스

## Vue Instance

{% file src="../.gitbook/assets/index.html" caption="이번장의 코드입니다." %}

먼저 뷰 인스턴스에는 무엇이 있는지 콘솔로 확인을 해보겠습니다 . 

```markup
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>
<body>
    <div id="app">
        <div>{{msgA}} </div>
        <button>Change!</button>
    </div>
    <script>
        const vm = new Vue({
            el:'#app',
            data:{
                msgA:'Message A.'
            },
            methods:{
                changeMessage(){
                    this.msgA = 'changed Message A!'
                }
            }
        })
        console.log(vm);
    </script>
</body>
</html>
```

![&#xBDF0;&#xC5D0;&#xC11C; &#xC0AC;&#xC6A9; &#xAC00;&#xB2A5;&#xD55C; &#xB2E4;&#xC591;&#xD55C; &#xAC83;&#xB4E4;&#xC774; &#xB4E4;&#xC5B4; &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;. ](../.gitbook/assets/image%20%281%29.png)

$가 표기된 것은 Vue안에 원래 들어있던 것들입니다. 

좀더 자세한 사항들이 궁금하면 아래 링크를 참고해주세요.

{% embed url="https://kr.vuejs.org/v2/api/\#%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4-%EC%86%8D%EC%84%B1" %}

자세히 보면 아래와 같이 작성한 내용도 들어있는걸 확인할 수 있습니다. 

![](../.gitbook/assets/image%20%2821%29.png)

### data

msgA는 Vue인스턴스를 생성할때 data로 만들어 주었습니다. 그리고 반응성을 가지고 있죠. 

하자만, Vue 인스턴스에 생성될때 정의되지 않은 데이터는 반응성을 가지지 않습니다.

한번 data가 아닌 메소드를 실행할때 msgB를 추가해 볼까요?  

```markup
<div>{{msgA}} </div>
<div>{{msgB}} </div>
 <script>
        const vm = new Vue({
            el:'#app',
            data:{
                msgA:'Message A.'
            },
            methods:{
                changeMessage(){
                    //this는 Vue를 가리킵니다. 
                    this.msgA = 'changed Message A!'
                    this.msgB = 'changed message B!'
                }
            }
        })
        console.log(vm);
    </script>
```

changeMessage메소드가 실행되면 Vue에 msgB가 생성이 되고 , 이는 문법적으로 전혀 문제가 없습니다.  

![](../.gitbook/assets/oct-26-2020-16-49-36.gif)

잘 실행은 되지만, msgB는 Vue가 생성될 당시에 생성된 것이 아닌, changeMessage메소드가 실행될때 생성이 된 것입니다.  **이렇게 생성된 데이터는 반응성을 가지지 않습니다!!** 

이는 Vue 개발자 도구를 설치하고 확인할 수 있습니다 . \(크롬, 파이어폭스 확장 프로그램\)

![vue&#xAC00; &#xAD00;&#xB9AC;&#xD558;&#xB294; Data&#xC5D0; msgB&#xAC00; &#xC5C6;&#xC2B5;&#xB2C8;&#xB2E4;. ](../.gitbook/assets/image%20%2811%29.png)

그러므로 반응성을 가지게 하기 위해서는 아래와 같이 빈 값이라도 생성을 해놓는것이 반응성을 가지게 할 수 있는 방법입니다 . 

```markup
data:{
   msgA:'Message A.',
   msgB:''
},
```

### computed , watch

사용할 데이터를 위에서 data instance를 통해 생성해 주었는데, 이는 사실 원시데이터에 가깝습니다. 

computed 는 계산된 데이터입니다.  =&gt; 기존의 데이터를 계산을 해서 화면에 그리는 것

watch는 데이터가 생성될때 원래 반응성을 가지게 하는데, 그 데이터가 반응성이 일어날때 즉, 변경될 때마다 watch에 있는 함수가 실행됩니다. 

```markup
watch:{
     msgA(value){
        console.log('watch:',value)
     }
}
```

위 코드는 msgA의 값이 변경될때마다 콘솔로 `watch: 바뀐 데이터`형식으로 찍어줍니다. 한번 실행해 보세요. 

![](../.gitbook/assets/image%20%283%29.png)



