# nodo server
서버에 대한 기본적인 구조와 서버를 만들어가는 과정에 대해 학습해 보고 스프린트 과제를 통해 실습해 보겠습니다.
<br />

## 1. 노드 서버의 기본적인 구조
서버는 크게 `http`모듈, `createServer` `listen`으로 기본적으로 구성 할수 있습니다.

```js
// 1. http 모듈 불러오기 및 기본 셋팅 하기
let http = require('http') // http 모듈을 불러옵니다.

const PORT = 3000; // 사용할 포트 번호 설정
const ip = 'localhost'; // 기본적으로 사용하는 ip주소

// 2. http 모듈로 서버를 생성 합니다.
const server = http.createServer((request, response) => { //인자는 req, res로 받습니다.
  response.writeHead(200, {'Content-Type':'text/html'}); // 상태 응답
  response.end('hello server'); //end는 선택적으로 데이터를 전달할 수 있습니다.
});

// 3. listen은 포트와 ip가를 통해 서버가 실행이 되었는지 확인해주는 함수입니다.
server.listen(PORT, ip, () => {
  console.log(`http server listen on ${ip}:${PORT}`);
});

```
<br /> 

1. 서버 사용을 위해서는 http 모듈을 `require`을 통해 불러옵니다 (변수명은 자유롭게 해도 상관 없습니다.) 그리고 PORT 와 ip는 변수로 미리 만들어 줍시다! (안해도 상관없습니다)

2. `createServer`는 서버를 만들어주는 메서드이고 req와 res을 인자로 받습니다. 즉 응답과 요청입니다.  
writeHead는 첫번째 인자는 상태 코드, 두번째 인자는 {키:값}형태의 값을 담습니다. (헤더값이라 생각하기)  
두번째 인자를 기준으로 화면이 출력 됩니다

3. listen 메서드 활용해서 서버가 잘 실행이 되었는지 확인 할수 있습니다. 이를 잘 확인하고 싶으면 콘솔창을 사용해서 터미널창에 콘솔창이 잘찍혔는지 확인하면 됩니다.
<br />

## 2. 기본 템플릿
프리플라잇트 헤더가 작성된 기본 템플릿 입니다. 이걸 바탕으로 서버를 구축 해보시길!

```js
let http = require('http') 

const PORT = 3000; 
const ip = 'localhost'; 


const server = http.createServer((request, response) => { 
  response.writeHead(200, defaultCorsHeader); 
  response.end('hello server'); 
});


server.listen(PORT, ip, () => {
  console.log(`http server listen on ${ip}:${PORT}`);
});

//cors 설정
const defaultCorsHeader = {
  'Access-Control-Allow-Origin': '*',
  'Access-Control-Allow-Methods': 'GET, POST, PUT, DELETE, OPTIONS',
  'Access-Control-Allow-Headers': 'Content-Type, Accept',
  'Access-Control-Max-Age': 10
};

```