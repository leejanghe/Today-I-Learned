## server_basic

---

## 서버를 띄우기 위한 기본 셋팅(express 라이브러리)

```js
const express = require('express'); //라이브러리 첨부
const app = express(); // 사용

// 원하는 포트에 서버를 오픈하는 문법
// listen(서버오픈포트번호, ()=>{서버오픈시 실행할 코드})
app.listen(8080,()=>{
    console.log("서버 실행 8080")
});

// get요청 (/경로, (요청,응답))
app.get('/pet',(req,res)=>{
    res.send('안뇽하세요 반갑습니땅!')
})

app.get('/beauty',(req,res)=>{
    res.send('뷰티사세염~@~@')
})
```

<br />

## 포트

포트는 외부와 통신 할수 있는 채널을 포트라고 부릅니다.

<br />

## 서버끄는 단축키

터미널에서 서버를 끈 다음에 다시 node 파일명 입력해서 서버를 시작해야 합니다. (노드몬 쓰면 그냥 해결)

```js
컨트롤 + C
```
