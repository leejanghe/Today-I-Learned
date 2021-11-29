## vue의 데이터 바인딩 문법

뷰는 데이터 보관이 용의하고 보관한 데이터를 {{데이터}} 문법으로 감싸서 넣으면 끝이다. 아래는 뷰의 기본적인 틀입니다.

```js
<template>
  <img alt="Vue logo" src="./assets/logo.png">
</template>

<script>


export default {
  name: 'App',
  components: {
   
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
```

template에서는 HTML코드들을 작성하면 되고 자바스크립트는 script 스타일은 style에서 코드를 작성하면 됩니다.

<br />

## 중요 포인트

데이터 보관함은 아래와 같고 object 형식으로 저장하면 된다. 즉 스크립트 태그 안에 data(){return{}} 이걸 열고 데이터를 오브잭트 형식으로 저장하면 됩니다. 이것이 뷰의 데이터 보관함, 변수보관함이 됩니다. 아래 예를 들어 데이터 보관함에 price 정보를 넣었다고 가정하고 {{price}}를 활용해서 html 데이터 바인딩이 가능하다.

```js
<template>
  <img alt="Vue logo" src="./assets/logo.png">
    <p>{{ price }} 만원</p>
  </div>
</template>


export default {
  name: 'App',
  data(){
      return {
          // 객체형태로
          price : "50"
      }
  },
  components: {
   
  }
}
```

또 한 스타일 또 한 class, id 이런 것들에도 데이터 바인딩이 가능합니다. 규칙은 태그에 :style="데이터변수" 로 작성하면 됩니다. 

```js
<template>
  <img alt="Vue logo" src="./assets/logo.png">
    <p :style="colorStyle">{{ price }} 만원</p>
  </div>
</template>


export default {
  name: 'App',
  data(){
      return {
          // 객체형태로
          price : "50",
          colorStyle : 'color:red'
      }
  },
  components: {
   
  }
}
```

