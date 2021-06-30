## Express

---

Express는 Node.js를 빠르고 간결하게 사용하기 위해 만들어진 웹 프레임워크입니다! 프레임워크는 이미 구현이 되어 있는 것을 말합니다!!! 그래서 일반적으로 서버를 만들때 보다 Express프레임 워크를 활용하면 좀더 유용하게 서버를 구현할수 있습니다!! 많이 사용하고 있는 프레임워크이니 꼭 알고 넘어 갑시다!
<br />

## Express 설치

---
<br >

```js
$ npm install express
```
좀더 자세한 방법을 알고 싶으면 [Express_설치링크](https://expressjs.com/ko/starter/installing.html)확인하기!
<br />

## Express 사용하기

---

아래 코드는 express를 사용하기 위한 기본 구조입니다.

```js
// express 기본 구조
 
const express = require('express')  // express 불러오기
const app = express()  // 불러운 express함수를 app 담아 쓰기
const port = 3000 
 
 
app.listen(port, () => {  // listen은 서버 대기라고 생각하면 됩니다.
  console.log(`Example app listening at http://localhost:${port}`)
})

```
### 사용예제

```js
const express = require('express')
const app = express()
const port = 3000
 
app.get('/', (req, res) => {
  res.send('joycoding!')
})
 
app.listen(port, () => {
  console.log('저는 대기 후 출력됩니다!')
})
```
<br>
위코드를 실행시키면 터미널에는 "저는 대기 후 출력됩니다!"가 찍히고 브라우저에서는 "joycoding!"이 출력됩니다. 여기서 5,6번 줄은 기본적인 라우팅 입니다. get이라는 요청 메서드를 사용하였고 '/' 경로와 콜백함수 인자 req, res 를 사용합니다. (req, res 는 요청과 응답이라고 생각하면 됩니다) 6번줄의 res.send는 응답할 데이터를 보내줍니다.

<br />

## Express 기본 라우팅

---

app은 express의 인스턴스입니다.  
메서드는 HTTP 요청 메소드 입니다. (Get, Post, Put, Delete)PATH는 서버에서의 경로입니다.HANDLER는 라우트가 일치할 때 실행되는 콜백 함수입니다.
<br >

```js
app.메서드(PAHT,HANDLER) // 기본 라우터 형식
```
### 사용예제
```js
// get
// 홈 페이지에서 Hello World!로 응답:
app.get('/', function (req, res) {
  res.send('Hello World!');
});
 
// post
// 애플리케이션의 홈 페이지인 루트 라우트(/)에서 POST 요청에 응답:
app.post('/', function (req, res) {
  res.send('Got a POST request');
});
 
// put
// /user 라우트에 대한 PUT 요청에 응답:
app.put('/user', function (req, res) {
  res.send('Got a PUT request at /user');
});
 
// delete
// /user 라우트에 대한 DELETE 요청에 응답:
app.delete('/user', function (req, res) {
  res.send('Got a DELETE request at /user');
});

```
<br />

## Express 정적 파일 제공

---

```js
app.use(express.static('public'));
```
이미지, CSS 파일 및 자바스크립트 파일과 같은 정적 파일을 제공하려면 미들웨어 함수인 `express.static`을 사용하면 됩니다. 여기서 'public'은 하나의 디렉토리 파일이고 이폴더 안에 html, css, js파일이 들어 있다라고 생각하면 됩니다.
<br />

```js
app.use('/static', express.static(__dirname + '/public'));
```
더 좋은 방법으로는 `__dirname + 절대경로`를 활용해서 사용하면 더 안정적으로 파일을 불러 올수 있습니다. 위와 같은 방법으로 파일을 불러오는 것을 권장합니다!
<br />


지금까지 기본적인 내용만 정리하였고 [express](https://expressjs.com/)에 자세한 사항은 공식문서를 참고해서 공부하면 더 좋을것 같습니다!
