## 컴포넌트 만들기

뷰에서 컴포넌트 만드는 방법은 엄청 간단합니다. 간단한 규칙만 알면 쉽게 만들수 있습니다.

<br />

### 1. 컴포넌트 뷰파일 만들기

우선 파일을 하나 만들고 < 엔터를 클릭하면 뷰 파일 형식이 자동으로 나옵니다. 

```js
// 컴포넌트 파일
<template>

축약할 html

</template>

<script>
export default {
    name: "작명",
}
</script>

<style>

넣을 스타일

</style>
```

<br />

### 2. import하고 등록하고 사용하기

우선 전에 만들었던 컴포넌트 파일을 import하고 스크립트에서 컴포넌트 파일을 등록한다음 사용하면 됩니다.

```js
// 3. 사용하기
<작명 />


// 1. import
import 작명 from '컴포넌트 만든 경로'

export default {
  name: 'App',
  data(){
  },
 
  },
  //2. 컴포넌트 등록하기
  components: {
    작명 : 작명,
   
  }
}
```

<br />
