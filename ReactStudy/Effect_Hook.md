## Effect Hook

---

Effect Hook은 리엑트에서 제공하는 useEffect라고 생각하면 됩니다. useEffect는 컴포넌트 내에서 Side effect를 실행 할 수 있게 하는 Hook입니다.
<br />

## 언제 실행하나요 ?

---

`useEffect`의 첫번째 인자는 함수입니다. 해당 함수 내에서 side effect를 실행 하면 됩니다.  
다음 예제를 통해 어떤 조건에 실행 되는지 확인해 봅시다!!!
<br />

```js
import React, {useEffect} from 'react';

function App(){

    useEffect(()=>{
        console.log('effect')
    })
        console.log('rendering')
    return (
        <div>hello!</div>
    )
}


export default App;
```

위에 있는 예시에 콘솔창을 확인하면 `rendering`이 먼저 찍히고 그다음 `effect`가 찍히는 것을 확인할수 있습니다. 다음과 같이 useEffect가 실행하는 3가지 조건이 있습니다.  
1. 컴포넌트 생성 후 처음 화면에 렌더링 (표시)<br />
2. 컴포넌트에 새로운 props가 전달되 며 렌더링<br />
3. 컴포넌트에 상태(state)가 바뀌며 렌더링<br />

이와 같이 매 번 새롭게 컴포넌트가 렌더링 될때 Effect Hook이 실행 됩니다.<br />

주의할점은 최상위에서만 Hook을 호출하고 React함수 내에서 Hook을 호출 합니다!
<br />

## 조건부 effect 발생 dependency array

---

useEffect의 두번째 인자는 배열 입니다. 이 배열은 조건을 담고 있습니다. 여기서 조건은 true, false가 아닌, 어떤 값의 변경이 일어날 때를 의미 합니다. 따라서, 해당 배열엔 어떤 값의 목록이 들어갑니다. 이 배열을 종속성 배열이라고도 부릅니다.<br />

다음 예제를 통해 조건부 effect에 대해 알아 봅시다!!!

```js
import React, {useEffect,useState} from 'react';

function App(){
    const [count, setCount] = useState(0)
    const [count1, setCount1] = useState(0)

    useEffect(()=>{
        console.log(count)
    },[count,count1]) // 여기 조작해보기
 
       console.log('rendering')
    const upNum = () => {
        setCount(count+1)
    }

    const upNum1 = () => {
      setCount1(count1+1)
  }

    return (
        <>
        <h1>숫자 : {count}</h1>
        <button onClick={upNum}>Click</button>
        <h1>숫자 : {count1}</h1>
        <button onClick={upNum1}>Click</button>
        </>
    )
}


export default App;

```

위에 있는 예제에 `dependency array` 조작하여 콘솔창의 변화를 확인해 봅시다!!!  

지금 있는 예제에서 count1을 제거하고 첫번째 클릭버튼을 클릭하면 렌더링은 한번만 호출되고 숫자가 증가하는 콘솔창을 볼수 있습니다 반면에 두번째 클릭 버튼을 클릭하면 렌더링 콘솔창만 찍히는 것을 확인 할 수 있습니다! 그래서 `dependency array`내의 종속성의 값이 변할 때 effect가 발생하는 함수가 실행 된다 는 것을 알수 있습니다! 
