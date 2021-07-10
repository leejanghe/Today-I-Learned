# 리엑트 리덕스로 간단한 카운터 만들기

---

## 리덕스 설치하기

---

해당 프로잭트에 redux와 react-redux 라이브러리를 설치합니다.

```js
$npm instail redux react-redux
```

react-redux 라이브러리에서는 useSelector와 useDispatch Hooks와 Provider 컴포넌트를 사용할수 있습니다.
<br />

<br />

## 리덕스 코드 작성하기(액션, 액션 생성 함수, 리듀스)

---

간단한 예제이기때문에 덕스 패턴으로 정리하겠습니다!!! 규모가 큰 프로젝트면 분리해서 작업하는것을 권장합니다! 덕스패턴이란 액션(Action Type), 액션 생성 함수, 리듀서(Reducer)를 하나의 파일안에 작성하는 것을 의미합니다.

<br />

```js
// 액션 생성
// 액션을 생성할때 대문자로 작성하는것은 개발자 사이에서 암묵적 약속입니다.
const INCREASE = "COUNTER/INCREASE";
const DECREASE = "COUNTER/DECREASE";

// 액션 생성 함수
// 액션은 객체로 구성되어 있고 type이 명시적으로 작성되어야 합니다.
export const increaseCount = () => {
  return { type: INCREASE };
};

export const decreaseCount = () => {
  return { type: DECREASE };
};

// 초기 설정
// default parameter 인자로 초기값을 설정할수 있습니다.
const initState = {
  count: 0,
};

// 리듀서
// 리듀서는 switch case 문으로 작성하는것이 매우 편합니다.
export default function Reducer(state = initState, action) {
  switch (action.type) {
    case INCREASE:
      return {
        ...state,
        num: state.count + 1,
      };
    case DECREASE:
      return {
        ...state,
        num: state.count - 1,
      };
    default:
      return state
  }
}

```
<br />


## 카운터컴포넌트 작성

---

react-redux 라이브러리에서 제공하는 useSelector를 사용하여 store에 저장되어 있는 데이터를 가져올 수 있습니다. 아래 코드에서는 count의 값을 가져옵니다. 위에서 초기값 설정한 값 0이겠죠 ? 또한, useDispatch를 사용하여 해당 액션을 실행시켜 줄 수 있습니다.
<br />

```js
import {useDispatch, useSelector} from "react-redux";
import {decreaseCount, increaseCount} from "../Reducer/Counter";
import React from 'react';

const Counter = () => {

    const count = useSelector(state =>  state.count);
    const dispatch = useDispatch();

    return (
        <div>
            <h1>카운터입니다!</h1>
            <div> {count} </div>
            <br />
            <button onClick={() => dispatch(increaseCount())}> + </button>
            <button onClick={() => dispatch(decreaseCount())}> - </button>
        </div>
    );
};

export default Counter;
```
<br />

## App.js

```js
import "./App.css";
import React from "react";
import Counter from "./Component/Counter";

function App() {
  return <Counter />;
}

export default App;
```
<br />



## index.js에서 store연동 작업

---

Provider 컴포넌트 안쪽에 연동할 컴포넌트를 감싸 넣어준 후, Provider 컴포넌트의 props로 store을 아래와 같이 설정해주면 됩니다. createStore 인자는 액션을 실행시켜줄 리듀서를 넣으면 됩니다.

```js
//...생략
import {Reducer} from "./Reducer/Counter";
import { createStore } from "redux";
import {Provider} from "react-redux";

const store = createStore(Reducer);
ReactDOM.render(
    <Provider store = {store}>
    <App />
    </Provider>,
  document.getElementById('root')
);
```

