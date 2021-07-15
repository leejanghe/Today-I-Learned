## default parameter

---

default parameter는 자바스크립트에서 추가된 ES6 신문법입니다. 함수를 만들 때 파라미터 값을 생략하고 싶을때 파라미터 default값을 줄수 있습니다.

```js
// 파라미터(인자) 생략
// 파라미터가 정의되지 않았을 경우에 등호 오른쪽 값이 실행됩니다.
function add(a, b=5){
    console.log(a+b)
}
add(1)    //6

// 생략을 안하면 인자값을 우선으로 합니다
function add(a, b=5){
    console.log(a+b)
}
add(1,7)  //8
```

<br />

## 함수도 default값으로 넣을수 있습니당

default parameter에 함수 입력도 가능합니다.

```js
function seven(){
    return 7
}

function add(a, b=seven()){
    console.log(a+b)
}

add(7) //14
```