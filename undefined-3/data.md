# 컴포넌트의 data가 함수인 이유

우리는 컴포넌트를 만들때 아래와 같이 만들었어요.

```javascript
const myComp ={
      template:"<div class='me'>{{messaga}}</div>",
      data:function(){
        return{
            messaga:'Hello Vue!',
        }
    }
}
```

컴포넌트의 데이터를 함수로 만들고, 

특정한 데이터 \(객체\) 를 가지고 있는 것을 리턴해 주었습니다. 

{% embed url="https://kr.vuejs.org/v2/guide/components.html\#data-%EB%8A%94-%EB%B0%98%EB%93%9C%EC%8B%9C-%ED%95%A8%EC%88%98%EC%97%AC%EC%95%BC%ED%95%A9%EB%8B%88%EB%8B%A4" %}

컴포넌트는 재사용이 가능합니다. 

만약 데이터에 일반 참조형 객체데이터를 입력해주면 불변성을 가지지 않게되서, 여러 컴포넌트에서 한 객체데이터를 같이 쓰게 됩니다. 

> 즉, 한가지 컴포넌트에서 데이터를 변경하면 모든 컴포넌트에 데이터가 변경되는 것입니다.

### Immutable

불변성은 모던한 프레임워크에 있어서 매우 중요한 부분입니다. 

```javascript
let a = "Hello";
console.log(a); // 'Hello'

let b = a;
console.log(a, b); //'Hello','Hello'

a = "Good";
console.log(a, b); //'Good','Hello'
```

a데이터 값을 바꾸어 줬지만, b값에는 변화가 없습니다. 즉, 완전 별개의 데이터가 되는 것이죠. 

> 원시데이터의 경우가 불변성을 가진 데이터입니다.

하지만, 객체데이터, 배열데이터 같은 경우에는 같은 곳을 참조하는 경우가있습니다. 

```javascript
let a = {h: "hello"};
console.log(a); //{h: "hello"}

let b = a;
console.log(a, b); //{h: "hello"},{h: "hello"}

a.h = "Good";
console.log(a, b); //{h: "Good"},{h: "Good"}
```

이러한 Object형태의 데이터들은 각은 곳을 참조하고 있어서 불변성을 가지지 않습니다. 

이부분은 나중에 추가설명 하겠습니다. 



아무튼 !! 

함수를 통해 컴포넌트마다 함수를 통해 새로 생성해 주어서 다른 곳을 참조하도록 만들어서 각각의 데이터를 가지게끔 만들어 주는 것입니다. 

또한 앞으로는 컴포넌트 뿐만아니라 모든 데이터를 무조건 함수로 작성해주면 되겠습니다! 

```javascript
const myComp ={
      template:"<div class='me'>{{messaga}}</div>",
      data(){
        return{
            messaga:'Hello Vue!',
        }
    }
}
```



