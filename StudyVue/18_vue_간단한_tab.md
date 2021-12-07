## vue로 간단한 tab 만들기

우선 모달 만드는 방법과 거의 흡사하다. 그리고 리엑트보다 훨씬 간단하게 만들수 있는게 장점이다. 


<br />

### 1. 텝을 데이터 저장

우선 데이터에서 상태 관리를 0으로 해준다.

```js
data(){
    return {
      step : 0,
    }
  },
```

<br />

### 2. v-if 조건문 사용

v-if 조건문을 활용해서 0일때 0내용이 나오고 1일때 1내용이 나오는 식으로 간단하게 만들수 있습니다.

```html
<div v-if="step === 0">내용0</div>
<div v-if="step === 1">내용1</div>
<div v-if="step === 2">내용2</div>
<button @click="step = 0">버튼0</button>
<button @click="step = 1">버튼1</button>
<button @click="step = 2">버튼2</button>
```
