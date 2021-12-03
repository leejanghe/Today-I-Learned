## v-model 사용법

v-model 은 자바스크립트에서 input값의 value를 가져오는 거랑 매우 흡사합니다. 즉 event.target.value라 생각하면 좋습니다. 일반적인 예시로는 아래와 같습니다.

```js
data(){
        return {
            month : 1,
        }
    },
```

우선 초기값을 나타내는 데이터를 보관함을 만듭니다.

```html
 <!-- <input v-model.number="month"> -->
    <input @input="month = $event.target.value">
    <p > {{month}}개월 선택함 : {{ oneroom[clickModal].price * month}} 원</p>
    <button @click="close" >닫기</button>
```  

그다음 위와 같이 @input이나 @onchange 이벤트 헨들러를 사용하면 됩니다. 만약 이걸 축약 하고 싶을 때 v-model을 쓰면 됩니다.

```html
    <input v-model.number="month">
    <p > {{month}}개월 선택함 : {{ oneroom[clickModal].price * month}} 원</p>
    <button @click="close" >닫기</button>
```  