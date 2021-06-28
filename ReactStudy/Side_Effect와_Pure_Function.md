## Side Effect(부수 효과)

---

함수 내에서 어떤 구현이 외부에 영향을 끼치는 경우 Side Effect라고 합니다.</br>
다음 예제를 통해 Side Effect대해 이해 해봅시다!</br>

```js
let foo = "hello world"

const bar =()=>{
    foo = "joycoding"
}

foo // bar를 실행하지 않을때는 기존 "hello world" 출력됩니다.
bar(); // bar를 실행 하면 어떻게 될까요 ?
foo // foo를 다시 실행 할때 "Joycoding"이 출력 됩니다.

```
위에 있는 예제에서 bar는 함수내부에 있는 로직이 외부에 영향을 끼쳐 Side Effect를 발생시키십니다.
</br>

## Pure Function(순수 함수)

---

순수 함수는 오직 함수의 입력만이 함수의 결과에 영향을 주는 함수를 의미합니다.  
또한 순수함 수는 입력으로 전달된 값을 수정하지 않습니다.  
다음 예제를 통해 Pure Function대해 이해 해봅시다!</br>

```js

let str = 'joycoding'

function upper(str){
    return str.toUpperCase(); // 원본수정x (Immutable)
}

upper(str) // 'JOYCODING'
str // 'joycoding'

```

</br>

### Side Effect와 순수 함수를 알아하는 이유

React에서 비동기 처리할 일들이 있습니다. 즉 로딩화면을 구현하거나 AJAX요청, 타이머 사용(setTimeout), fetch API 등 이는 Side Effet를 발생시킵니다. 그래서 이것들을 다루기 위해서 리엑트에서는 Hook인 Effect Hook을 제공합니다. 그러니 side effect와 순수 함수에 대한 원리를 꼭 알고 넘어 갑시다!