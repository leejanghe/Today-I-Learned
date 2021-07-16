# 개요
이번 3일동안 서버를 공부하면서 알게된 잡지식을 정리해보고자 합니다!!!
<br />

---

## 1. 디버거 하는 방법!!!
아래와 같이 터미널에 `$node --inspect-brl 폴더명/파일명` 실행하면 브라우저 네트워크에서 디버깅을 할 수 있습니다!
<br />

```js
$node --inspect-brl 폴더명/파일명
```

---

## 2. 서버 응답요청하기 
서버에 응답을 할때 `res.end` `res.send()` `res.json()` 이것을 썼습니다! 결론부터 말하자면 셋다 응답을 나타내는 같은 의미 입니다.

<br />

```js

res.send() // 기본적인 사용
res.end()  // 데이터 없이 신속하게 응답을 종료 할때
res.json() // application/json // 제이슨 응답을 할때 이거 많이 씁니다
// 우리가 서버 언어를 주고 받을때 통상적으로 제이슨으로 주고 받습니다! 이거 많이 씁시당
```
<br />
이외 공식문서를 확인하면 응답하는 메서드가 참 많습니다!

---

## 3. 라우터 사용
라우터는 객체 미들웨어 및 경로의 고립 된 인스턴스입니다. 한파일에서 써도 상관 없지만 분류해서 정리하는게 유지보수하기 더 효율 적입니다! 그래서 app.js에서 use()를 사용해서 경로를 등록하고 해당 경로 라우터파일에서 라우터 모듈을 받아서 합시다!

<br />

```js
//app.js
//...생략

app.use('/hello', 라우터관리파일)  // use() 미들웨어로 라우터 경로를 등록 해줍니다.


//라우터관리파일
//...생략
const router = express.Router() // 라우터 파일에서 라우터 모듈 가져와서 쓰면 됩니다 다이어져 있습니다.

router.get('/' ,(req, res, next)=>{
    //로직 작성하기
})

```
<br />
라우터를 사용할때는 분리해서 쓰는 습관을 기릅시다!

---

## 4. req.query와 req.params 비교하기
그냥 쉽게 생각해서 req.query는 빈객체라고 생각하면 너무나 편하고 이 빈객체를 활용해서 데이터를 어떻게 요청하고 응답할지 생각하면서 로직을 작성하면 됩니다!

<br />

```js
//GET /search?q=joycoding
console.log(req.query.q) // 'joycoding'

// 정말 쉽게 자바스크립트로 표현하자면
obj = {} //여기서 obj를 req.query 로 생각하기!
obj.p = 'joycoding'
obj // {p:"joycoding"}

```
<br />
그러면 req.params는 무엇일까요 ? req.query와 완전 다른 개념입니다! req.params는 쉽게 말해 /:id , /:name 처럼 이런 모양이면 req.params을 활용해서 쓸수 있다 라고 쉽게 생각하면 좋습니다. req.query와 req.params 비교해보겠습니다.
<br />

```js
//경로가 /user/:name 일경우
//GEt /user/joycoding
consolo.dir(req.params.name) // joycoding


// req.query와 req.params 비교
// req.query
// localhsot:3000/joycoding?page=hello
app.get('/joycoding',(req, res)=>{
    req.send(req.query.page); //req.query.page=hello
});

// req.params
// localhsot:3000/joycoding/hello
app.get('/joycoding/:page',(req, res)=>{
    req.send(req.params.page); //req.params.page=hello
});

```