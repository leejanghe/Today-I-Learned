## vuex action

vuex에서 상태를 수정할때 mutations함수를 활용해 수정합니다. 하지만 서버에서 데이터를 가져와서 데이터를 수정하고 싶을때가 있습니다. 이때 mutation이 아닌 actions라는 항목에 작성해서 사용하면 됩니다.

<br />

### actions step 1

우선 데이터를 보관함을 만들어 줍니다.

```js
// store.js
import (createStore) from 'vuex`

const store = createStore({
    state(){
        return {
            more : {},
        }
    },
})
```

<br />

### actions step 2

state를 수정하는 함수는 mutations에다 작성하고 ajax요청은 넣지 않습니다. actions에서 다해주기 때문입니다.

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
      mutations:{
        setMore(state , data){
            state.more = data
        },
})
```

<br />

### actions step3

mutations함수를 사용할 땐 예외없이 commit()라고 써야합니다. 그리고 그걸 쓰기 위해선 함수에 context라는 파라미터를 추가해주면 됩니다. context 대신 작명 가능하며 $store 변수 같은거라고 생각하면 됩니다.

```js
// store.js
const store = createStore({
    state(){
        return {
            more : {},
        }
    },
    mutations:{
        setMore(state , data){
            state.more = data
        },
    },
    actions : {
        getData(context){
            axios.get(`요청코드`)
            .then((a)=>{
                //성공시 실행할 코드
                console.log(a.data) 
                context.commit('setMore', a.data)
            })
        },
    },
})
```

<br />

### actions step 4

actions 항목을 다만들었으면 $store.dispatch('action함수이름') 를 사용해서 데이터를 가져옵니다.

```html
<!-- app.vue -->
<p>{{$store.state.more}}</p>
<button @click="$store.dispatch('getData')">더보기버튼</button>
```