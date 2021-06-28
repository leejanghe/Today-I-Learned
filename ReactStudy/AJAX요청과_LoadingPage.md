## AJAX요청과 LoadingPage

---

아래에 있는 예시 코드는 useEffect를 활용한 AJAX요청 기본적인 템플릿 입니다.
<br />

```js
useEffect(()=>{
    fetch('url 주소')
    .then(res => res.json())
    .then(data => {
        실행할변경함수(data)
    })
},[종속조건 배열])

```
<br />

### LoadingPage를 구현하고 싶다면 ?

로딩페이지를 구현하기 위해선 상태 처리가 필요합니다.  

```js
const [isLoading, setIsLoading] = useState(true);
// 생략 로딩페이지 컴포넌트가 LoadingPage라고 가정

return {isLoading? <LoadingPage /> : <div>로딩 완료 페이지!</div>}

```
  
위에 있는 로딩상태처리를 하였으면 아래와 같이 useEffect와 같이 사용 할 수 있습니다.  

```js
useEffect(()=>{
    setIsLoading(true)
    fetch('url 주소')
    .then(res => res.json())
    .then(data => {
        실행할변경함수(data)
        setIsLoading(false)
    })
},[종속조건 배열])

```

## 예제를 통해 이해해보기

---

아래 코드는 ajax요청 대신 setTimeout 함수를 사용해서 구현하였습니다. 어떤 원리인지 콘솔창을 확인하면서 흐름을 파악하면 좋을것 같습니다!


```js
import React, {useEffect,useState} from 'react';

function App(){
    const [isLoding, setIsLoding] = useState(true)
    const [count, setCount] = useState(0)

    useEffect(()=>{
        setTimeout(()=>{
          setIsLoding(true)
          setIsLoding(false)
        },3000)
        console.log(count)
    },[count])
 
    console.log('render')

    const upNum = () => {
      setCount(count+1)
  }

    return (
        <>
        <button onClick={upNum}>{count}</button>
        {isLoding?<LoadingPage/>:<div>로딩 끝!!</div>}
        </>
    )
}


function LoadingPage(){
  return (
    <>
    <div>로딩중입니다!!!!</div>
    </>
  )
}


export default App;
```