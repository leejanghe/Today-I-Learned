## API 키 숨기기

---

개인작업을 할때 API를 받아와서 작업하는 경우가 허다합니다! API를 받아 올때 본인의 개인 API키를 사용합니다. 그래서 본인의 API키를 그대로 깃헙에 올려 노출되는 경우가 있습니다! api키는 될수있으면 노출시키지 않고 올리는 것이 보안상 좋습니다. 그래서 이번 시간은 API키를 숨기는 방법에 대해 알아보겠습니다!
<br />

## 최상위 디렉토리에 .env 파일 만들기

---

최상위 디렉토리에 .env파일을 만들어 주고 파일안에 아래와 같이 작성합니다.
<br />

```js
REACT_APP_YOUTUBE_API_KEY={본인의 API키 작성}
```
<br />

## 인덱스js파일에서 변수 지정 및 전달하기

---

API키를 관리하는 파일을 불러오고 .env에서 지정 한 API KEY를 아래와 같이 변수에 담아주고 App컴포넌트에 전달합니다.
<br />

```js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import Youtube from './service/youtube'; //api키 관리 파일

const youtube = new Youtube(process.env.REACT_APP_YOUTUBE_API_KEY); //env파일에 있는거 쓰기
ReactDOM.render(
  <React.StrictMode>
    <App youtube={youtube}/>
  </React.StrictMode>,
  document.getElementById('root')
  ```
  <br />


## &{this.key}로 감싸 주기!

---

본인의 키를 다 아래와 같이 &{this.key}로 감싸줍시다!!!


<br />

```js
//...생략

fetch(`https://youtube.googleapis.com/...생략=${this.key}`,
//...생략
```

<br />

## 인덱스js파일에서 변수 지정 및 전달하기

---

API키를 관리하는 파일을 불러오고 .env에서 지정 한 API KEY를 아래와 같이 변수에 담아주고 App컴포넌트에 전달합니다.
<br />