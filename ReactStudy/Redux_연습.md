# 별의미 없는 리덕스 메모장

---


## 바닐라 자바스크립트 연습

```js
const redux = require('redux'); //리덕스 모듈 가져오기
const createStore = redux.createStore; //스토어 생성
const combineReducers = redux.combineReducers // 합치기

// action 
// action-types
const ADD_SUBSRIBER = 'ADD_SUBSRIBER'
const addSubsrcibar = () => {
    return {
        type: ADD_SUBSRIBER
    }
}

// 추가한거
// action 
// action-types
const ADD_VIEWCOUNT = 'ADD_VIEWCOUNT'
const addViewCount = () => {
    return {
        type: ADD_VIEWCOUNT
    }
}


// reducers
// 초기값설정
const initialState = {
    subscribers : 365
}
const reducer = (state=initialState, action)=>{
    switch(action.type){
        case ADD_SUBSRIBER:
            return {
                ...state,
                subscribers: state.subscribers + 1
            }
            default: return state
    }
}

// store
// 생성 스토어에 리듀서 넣기
const store = createStore(reducer)

console.log(store.getState()) // 어떤값있는지 확인

store.dispatch(addSubsrcibar())  // 실행

// ----------

store.subscribe(()=>{
    console.log('subscribe ===>>>', store.getState())
})

store.dispatch(addSubsrcibar())  // 실행
store.dispatch(addSubsrcibar())  // 실행
store.dispatch(addSubsrcibar())  // 실행
store.dispatch(addSubsrcibar())  // 실행


//-----------------
// 추가한거
const viewState = {
    viewCount : 100
}
const viewReducer = (state=viewState, action)=>{
    switch(action.type){
        case ADD_VIEWCOUNT:
            return {
                ...state,
                viewCount: state.viewCount + 1
            }
            default: return state
    }
}

//-----
// 추가한 리듀스 합치는 방법
const rootReducer = combineReducers({
    view: viewReducer,
    subscriber : reducer
})

const store = createStore(rootReducer)
```

------------------------
<br />

## 리엑트로 연습

---

### 액션 & 액션 생성함수 만들기

```js
export const ADD_NUM = 'ADD_NUM'
export const REMOVE_NUM = 'REMOVE_NUM'

export const addSubscriber = () => {
    return {
        type: ADD_NUM
    }
}

export const removeSubscriber = () => {
    return {
        type: REMOVE_NUM
    }
}
```

### 리듀서 작성

```js
import {ADD_NUM, REMOVE_NUM} from './action'


const initialState = {
    count: 0
}

const Reducer = (state=initialState, action) =>{
    switch(action.type){
        case ADD_NUM:
            return {
                ...state,
                count: state.count + 1
            }
        case REMOVE_NUM:
            return {
                ...state,
                count: state.count - 1
            }
            default: return state
    }
}

export default Reducer
```

### 컴포넌트에서 작업하기

```js
import React from 'react'
import {useDispatch, useSelector} from "react-redux";
import { addSubscriber, removeSubscriber } from '../redux/action'

const Testpage=() => {

    const count = useSelector(state =>  state.count);
    const dispatch = useDispatch();

    return (
        <div>
            <p>구독자: {count}</p>
            <button onClick={()=>dispatch(addSubscriber())}>+</button>
            <button onClick={()=>dispatch(removeSubscriber())}>-</button>
        </div>
    )
}


export default Testpage
```

### 스토어 만들기

```js
import {createStore} from 'redux'
import Reducer from '../redux/reducer'

const store = createStore(Reducer)

export default  store;
```

### Provider 연동작업하기

```js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import {Provider} from 'react-redux'
import store from './store/store';


ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);
```