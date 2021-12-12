## vuex mutations 

mutatuons는 데이터 수정방법을 정의합니다. 오브젝트 항목을 만든 다음에 거기다 state 수정 방법을 함수로 만들어 정의합니다. 예를 들어 vue파일에 어떤 버튼을 누루면 age라는 state를 1더해주는 기능을 만들고 싶을때 아래 예시와 같습니다.

```js
// store.js
import (createStore) from 'vuex`

const store = createStore({
    state(){
        return {
            name : 'Lee',
            age : 20,
        }
    },
    mutations :{
        plusAge(state){
            state.age++
        }
    },
})
```

plusAge()함수에 파라미터 state는 위에 있는 age상태 입니다. 그다음에 vue파일에서 버튼 누를때 age + 1을 해주고 싶을때 위에 함수를 통해 vue파일에서 부탁할 수있습니다.

```html
<!-- app.vue -->
<button @click="$store.commit('plusAge')">버튼</button>
```

vue파일은 $store.commit(함수명) 이런 형식에 맞춰 부탁 할 수 있습니다. 이게 vuex에 있는 state수정 방법입니다.