## Middleware

---

Middleware는 자동차 공장의 공정과 비슷합니다. 중복되는 불필요한 코드를 줄여주고 node.js로 구현한 서버보다 훨 씬 작업을 보다 쉽게 적용 할 수 있습니다. express의 아주 큰 장점입니다. Middleawre의 특징은 (req, res, next)로 인자를 받습니다.<br />

미들 웨어를 사용하는 상황<br />
1. 모든 요청에 대해 url이나 메소드를 확인할 때<br />
2. POST 요청 등에 포함된 body(payload)를 구조화할 때(쉽게 얻어내고자 할 때)<br />
3. 모든 요청/응답에 CORS 헤더를 붙여야할 때<br />
4. 요청 헤더에 사용자 인증 정보가 담겨있는지 확인할 때<br />
<br />


## Middleware 기본 원리

---

미들웨어는 req, res, next로 인자를 받습니다. 그중 미들웨어의 핵심 인자는 next입니다. next를 호출해야지 다음 미들웨어로 데이터를 전달 할 수 있습니다. 
<br />

```js
//...생략

const testmiddle = function(req, res, next){
  console.log('미들웨어 입니다.');
  next() // 이것을 생략하면 무한 로딩중 즉 next()는 다음 미들웨어로 데이터로 전달합니다.
}

app.use(testmiddle)

app.get('/', (req, res)=>{
  console.log('저는 get 요청입니다!')
  res.status(200).send('welcome!!')
})

```
<br/>
위와 같이 요청을 보내면 터미널에 콘솔창이 '미들웨어 입니다', '저는 겟 요청입니다!' 순으로 찍힙니다. 만약 next()를 호출하지 않으면 그 이후의 라우터핸들러와 미들웨어가 호출되지 않아 클라이언트는 멈춰있다 타임아웃에 걸립니다. 그냥 next()는 다음 공정을 진행하는 기계라고 생각하면 편합니다!

<br />


## cors 미들웨어

---

일반적인 node.js에서 cors 헤더를 붙이려면 일일이 writehead메서드를 사용해야하고 헤더를 매번 재정의해야 하는 불편함이 있습니다 또한 OPTIONS 메서드에 대한 라우팅 작업도 해야 됩니다.
<br />

```js
//...생략
const defaultCorsHeader = {
  'Access-Control-Allow-Origin': '*',
  'Access-Control-Allow-Methods': 'GET, POST, PUT, DELETE, OPTIONS',
  'Access-Control-Allow-Headers': 'Content-Type, Accept',
  'Access-Control-Max-Age': 10
};

// 생략
if (req.method === 'OPTIONS') {
  res.writeHead(201, defaultCorsHeader);
  res.end()
}
```
<br />
하지만 cors미들웨어를 사용하면 이 과정을 간단하게 처리 할 수 있어서 아주 편리합니다!!!

```js
//...생략
const cors = require('cors')

// 생략
app.use(cors()) // 이코드 한줄로 모든 요청에 대해 CORS 허용 
```
<br />


## 스프린트 예제로 이해하기

---

미들웨어는 위에서부터 아래로 순차적으로 진행 됩니다! 아래 예제를 통해 이해해 봅시다!


```js
//...생략

app.use(cors()); //이것도 미들웨어입니다! 한번에 CORS 허용!!
app.use(express.json()); // 제이슨 파싱을 해줘야 겠죠?

app.use((req,res,next)=>{ //포스트맨에서 get을 하고 경로를 hello 라고 하면 
  console.log(req.method) //아래 콘솔창은 get / hello 가찍힙니다!
  next() //생략하면 큰일!!!
})

app.get('/', (req, res) => {
  res.status(200).send('어서오고!');
});

app.use((req, res, next) => { 
  res.status(404).send('Not Found!'); //404에러가 났는데 그다음 과정이 필요 없겠죠 ?
});

app.use((err, req, res, next) => {  //에러를 처리할때는 첫번째 인자에 err를 써줍니다
  console.error(err.stack);
  res.status(500).send({
    message: 'Internal Server Error',
    stacktrace: err.toString()
  });
});

//...생략

```
<br />

### 요약 정리
미들웨어는 요청과 응답사이에 있는 중간 과정이고 위에서부터 순차적으로 그공정이 실행이 되고 미들웨어를 짤때는 넥스트를 꼭 찍어야 합니다. 마지막에 에러 처리 할 때는 첫번째 파라미터에 err를 붙입니다!

