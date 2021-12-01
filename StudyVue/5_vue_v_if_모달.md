## vue v-if를 활용한 모달창

우선 뷰에서 모달창을 만드는 기본적인 스텝이 있다. 첫번째는 현재 HTML UI의 상태를 데이터로 저장합니다.(지금 보이는지 안보이는지) 그다음 그 상태에 따라 HTML UI를 보여줄지 말지를 Vue 문법으로 작성하면 된다.

<br />

### 1. 현 모달창의 상태를 데이터로 저장한다.

```js
data(){
    return {
      isModal : false,
    }
  },
```

<br />

### 2. 데이터 상태에 따라 UI를 보여줄지 말지 뷰 문법으로 작성.

```html
<!-- 모달 -->
<div class="black-bg" v-if="isModal === true">
  <div class="white-bg">
    <h4>상세페이지임</h4>
    <p>상세페이지 내용임</p>
    <button @click="isModal = false">닫기</button>
  </div>
</div>
```

html태그 안에서 v-if="조건식" 을 사용 하면 됩니다.

```css
/* 모달 css */
body {
  margin : 0
}

div {
  box-sizing: border-box;
}

.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}

.white-bg{
  width:100%; background: white;
  border-radius: 8px;
  padding: 20px;
}
```

<br />

## v-else

추가적으로 v-if에 적은 조건식이 참이 아닐 경우에 v-else를 보여 줍니다. 조건에 따라서 이거 혹은 저거를 보여주고 싶을 때 사용합니다.

```html
<div v-if="1 === 2">
    joycoding
</div>
<div v-else>
    teemo
</div>
```