## Routing

---

웹에서 통상적으로 말하는 라우팅이란 사용자가 요청하는 url링크를 요청했을때 어떤 특정한 페이지로 연결 할 건지를 결정하는 메커니즘을 말합니다. 
<br />

## SPA

---

싱글페이지 어플리케이션 SPA는 리엑트에서 쉽게 만들수 있는 라이브러리 입니다. 싱글페이지 어플리케이션이란 하나의 url로 한번 페이지가 로딩되고 나면 그안에서 사용자가 다른페이지를 클릭하거나 링크를 클릭 했을 때 새로운 페이지가 열리는게 아니라 부분적인 내용만 업데이트 되는 것이 싱글페이지 어플리케이션 입니다.  

문제점은 각각의 영상마다 그화면을 북마크 할수 없습니다. 뒤로가기 앞으로가기 이런 내비게이션에 추가가 되지 않습니다 왜냐
그페이지 안에서 동작이 일어 났기 떄문입니다.  

이런것을 보완하기 위해서 싱글페이지 어플리케이션을 유지하면서 url을 붙일수 있는 해당하는 페이지로 바로 갈수 있고 북마크와 네비게이션을 추가가 가능한것이 리엑트 라우터 입니다. 
<br />

## Routing시작하기 및 세팅하기

---

터미널에 열고 아래와 같이 설치합시다!
<br />

```js
yarn add react-router-dom
//or
npm install react-router-dom
```
<br />

그리고 index.js파일에서 아래와 같이 세팅해줍시다!!!
<br />

```js
// ...생략
import {BrowserRouter} from 'react-router-dom'

ReactDOM.render(
  <React.StrictMode>
    <BrowserRouter>
    <App />
    </BrowserRouter>
  </React.StrictMode>,
  document.getElementById('root')
);
```

## 기본 예제

---

라우터 사용법은 의외로 간단합니다. 스위치 안에 라우터를 감싸고 라우터안에 해당 컴포넌트를 감싸주면 됩니다. 그리고 라우터에 해당 컴포넌트의 경로를 설정하면 됩니다! 다음 아래 기본 예제를 통해 이해하기!!  
<br />

자세한 사용방법은 [여기](https://reactrouter.com/web/guides/quick-start)에 확인하길!!

```js
//app.js
import {Route, Switch, Link} from 'react-router-dom'
import Home from './components/home';
import Profile from './components/profile';

function App() {
  return (
    <>
    <nav>
      <Link to ="/">Home</Link>
      <Link to ="/profile">profile</Link>
    </nav>
    <Switch>
      <Route path={['/', '/home']} exact>
      <Home/>
      </Route>

      <Route path="/profile">
         <Profile/>
      </Route>
    </Switch>
    </>
  );
}

export default App;
```

<br />

```js
import React from 'react'
import { useHistory } from 'react-router-dom'

function Home() {
    const history = useHistory();
    return (
        <div>
            <h1>home</h1>
            <button
            onClick={()=>(history.push('/profile'))}
            >go to profile</button>
        </div>
    )
}

export default Home
```

<br />

```js
import React from 'react'
import { useHistory } from 'react-router-dom'

function Profile() {
    const history = useHistory();
    return (
        <div>
        <h1>profile</h1>
        <button
        onClick={()=>(history.push('/home'))}
        >go to home</button>
    </div>
    )
}

export default Profile
```