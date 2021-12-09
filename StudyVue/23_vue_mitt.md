## mitt

mitt은 상위-상위 컴포넌트나 아니면 동떨어진 컴포넌트에 데이터를 전송 할 때 사용하면 매우 유용합니다. 사용법도 간단합니다. 우선 설치부터 하기!

```
npm i mitt
```

설치가 끝나면 main.js파일에 가서 mitt 환경 셋팅을 합니다.

```js
import { createApp } from 'vue'
import App from './App.vue'

// mitt 라이브 셋팅
import mitt from 'mitt'
let emitter = mitt();
let app = createApp(App);

// 글로벌한 변수 보관함
app.config.globalProperties.emitter = emitter;

app.mount('#app')
```

<br />

## 사용법

데이터 보내고 싶은 곳에 아래와 같이 작성합니다. this.emitter.emit하면 전송이 가능합니다.

```js
methods :{
        hello(){
            this.emitter.emit('작명','데이터')
        }
    },
```

그리고 데이터 수신하고 싶은 곳에서 아래와 같이 작성하면 됩니다.

```js
//...생략
 mounted(){
    this.emitter.on('작명',(a)=>{
        // 데이터 수신시 실행할 코드
        // a는 데이터
      console.log(a)
    })
  },
```

보통 수신하는 코드는 mounted()안에 적습니다. 이러면 위에 했던 내용을 수신 받을수 있습니다.