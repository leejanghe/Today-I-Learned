## Express framework

---

express에 대한 부가 설명 및 팁에 대해 작성하고자 합니다!!! express를 사용할때 아래와 같이 구간별로 나눠 주면서 작성하는 습관을 기릅시다!!!
<br />

```js
// 외부 모듈

// 내부 모듈

// 전역 변수

// 라우트 모듈

// 실행로직

// listen 꼭 정의
app.listen(port, ()=>{
    console.log("Start Server!!")
})
}
```

listen는 서버를 켜주는 함수라고 생각하면 됩니다! 첫번째 인자는 포트번호, 두번째 인자는 콜백함수로 서버가 시작할때 딱한번만 실행이 됩니다. 이거 안해주면 서버가 안켜집니다! 좀 더 유용한 팁을 말하자면 여기부분에 우리가 만든 서버에 대한 스펙들을 정리해서 넣을수가 있습니다! 그러면 이서버가 어떤 서버인지 파악하기 쉽겠죠 ?

<br />

## use메서드는 무엇일까 ?

---

use는 서버를 실행하기전에 express에 미리 등록하는 것을 의미합니다. 무엇인가를 선언하거나 설정할때 use를 적습니다. 다르게 말하면 미들웨어 입니다. 미들웨어 사용법은 다시 정리해서 올리겠습니다!

```js
// 외부 모듈
const express = require('express')
const cors = require('cors')

//전역 변수
const app = express();
const port = 5000;
const ip = 'localhost';
 
//실행 로직
app.use(express.json());
app.use(cors());
//use는 등록해주다라는 개념으로 이해하기!!! express에 나는 cors를 사용할거야!!!라고 알려줍니다.

```
<br />

## 이미구현된 http 메서드

---

express는 http메서들이 이미 구현 되어있습니다. 그래서 `app.메서드()`로 쉽게 구현할수 있습니다.

```js 
//실행 로직
app.use(express.json());
app.use(cors());

app.get('/joycoding',fuction(req, res){ 

})
//express 알아서 매칭을 해서 joycoding 등록을 해줍니다.

```

<br />

## status header를 따로 작성을 안해도 됩니다!

---

express는 정상적인 처리가 되면 알아서 status header(상태 처리)를 해줍니다.

```js 
app.get('/',fuction(req, res){ 
    res.status(200),send("hello joycoding") // 통상적인 방법
    // res.send("hello joycoding")) 상태코드를 작성안해도 전달이 됩니다.
    // 하지만 기본적으로 상태코드를 넣는 습관을 기릅시다!
})

app.listen(port, ()=>{
    console.log("Start Server!!")
})
```

<br />

## post요청을 할때 바디를 쉽게 가져와 쓸수 있습니다.

---

express는 req.body라는것을 지원을 해줍니다. 만약에 키값을 text라도 정의하고 싶으면 아래와 같이 표현할수 있습니다.

```js 
app.get('/',fuction(req, res){ 
    res.status(200),send("hello joycoding")
})

//여기부분 주목!
app.post('/hello',fuction(req, res){ 
    let buffer = req.body.text  //req.body는 express에서 제공한것이고 text는 임의로 정의한 것입니다.
    console.log(buffer)
    res.status(200,send(buffer)
});

app.listen(port, ()=>{
    console.log("Start Server!!")
})
```
<br />
만약 이번에 배운 소문자를 대문자로 바꿔주는 요청을 간단하게 구현하자면 아래와 같습니다.

```js 
app.get('/',fuction(req, res){ 
    res.status(200),send("hello joycoding")
})

//여기부분 주목!
app.post('/upper',fuction(req, res){ //upper api
    let buffer = req.body.text

    let upper = buffer.toUpperCase(); //구현하기
    res.status(200,send(upper)
});

app.listen(port, ()=>{
    console.log("Start Server!!")
})
```
<br />

## 구조분해할당해서 가독성 올리기!

---

express에서 제공한 body.req를 구조분해 할당을 해서 코드를 줄이고 가동성 좋은 코드를 작성할수 있습니다. 위에 있는 예제를 바탕으로 설명하자면 아래와 같습니다.
<br />

```js 
let {body} = req; // 구조분해

app.get('/',fuction(req, res){ 
    res.status(200),send("hello joycoding")
})

//여기부분 주목!
app.post('/upper',fuction(req, res){ //upper api
    //let buffer = req.body.text
    let buffer = body.text // 이렇게 쓸수 있어여!

    let upper = buffer.toUpperCase();
    res.status(200,send(upper)
});

app.listen(port, ()=>{
    console.log("Start Server!!")
})
```
<br />

### 정리

여기서 꼭 알아야할 내용들을 다시 정리하자면!!!<br />
1. express의 기본적인 구조를 분류하고 작성하기<br />
2. 우리가 무엇인가를 설정하거나 사용하고 싶을때는 `use`메서드를 쓰기!<br />
3. POST요청에서 req.body를 활용해서 응답할 로직 작성하기!<br />
4. 구조 분해 할당을 통해 가독성 높히기!!!<br />

이정도만 알고 넘어가도 충분히 express를 사용할수 있습니다!!!