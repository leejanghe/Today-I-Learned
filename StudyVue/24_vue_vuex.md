## vuex 사용법

vuex는 props와 custom event로 데이터 주고받는게 힘들때 사용합니다. vuex를 설치하면 js 파일하나에다 모든 데이터를 저장 할 수있습니다. 그럼 모든 컴포넌트를 그 데이터를 직접 꺼내고 수정할 수 있어 프롭스 필요없이 모든 컴포넌트가 데이터에 직접 접근이 가능합니다. 그리고 vue파일과 데이터, 규모가 클 때 사용합니다. 리엑트에서 리덕스 개념으로 생각하면 편합니다.

<br />

## vuex 셋팅

우선 터미널에서 vuex를 설치합니다.

```
npm i vuex@next --save
```

그리고 js파일을 만들어 아래와 같이 기본 셋팅을 합니다.

```js
// store.js
import (createStore) from 'vuex`

const store = createStore({
    state(){
        return {

        }
    },
})

export default store
```

그다음 store.js 파일을 main.js에 등록하면 됩니다. (꼭 등록해야합니다.)

```js
import store from './store.js'
app.use(store).mount('#app')
```

그럼 store.js에 저장한 데이터들을 모든 컴포넌트가 가져다 쓸 수 있습니다. 데이터 저장은 store.js에 저장하면 되고 출력하려면 vue파일에서 {{$store.state.데이터명}}해서 사용하면 됩니다. 