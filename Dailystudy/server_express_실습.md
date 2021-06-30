# server_express 실습하기
node_server로 구현한 upper / lower을 express를 프레임워크를 활용해서 리팩토링 해보겠습니다!
<br />

---

## node_server로 구현하기
아래는 node_server로 upper / lower 을 구현한 코드입니다. 
<br />

```js
const server = http.createServer((request, response) => {
if(request.method === "POST"){
  if(request.url === '/lower'){
    let data = "";

    request.on('data',(chunk)=>{ //on은 어떤 이벤트를 줄경우 콜백함수를 그에 맞춰 실행하는 메서드
      data = data + chunk        // 청크를 통해 바디값을 받아올 수 있다(단 on이라는 데이터 키워드를 넣어야 됨)
    })

    request.on('end',()=>{ // data와 end는 약속된 키워드 이벤트 입니다.
      data = data.toLowerCase() //4단계 동작구현
      response.writeHead(201, defaultCorsHeader);
      response.end(data) // end는 응답하기 위한 메서드
    })


  }else 
  if(request.url === '/upper'){
    let data = "";

    request.on('data',(chunk)=>{ //on은 어떤 이벤트를 줄경우 콜백함수를 그에 맞춰 실행하는 메서드
      data = data + chunk        // 청크를 통해 바디값을 받아올 수 있다(단 on이라는 데이터 키워드를 넣어야 됨)
    })

    request.on('end',()=>{ // data와 end는 약속된 키워드 이벤트 입니다.
      data = data.toUpperCase() //4단계 동작구현
      response.writeHead(201, defaultCorsHeader);
      response.end(data)
    })
  }else{
    response.writeHead(404, defaultCorsHeader);
    response.end("Not found 404");
  }
}


if(request.method === "OPTIONS"){ //프리플라이트 내용들을 해더에 보내줘야됨 
  response.writeHead(200, defaultCorsHeader);
  response.end() // 보내줄 데이터가 없고 여기 부분은 프리플라이트는 헤더에서 요청됨
  }

});
```
<br />

---

## express프레임 워크를 활용해서 구현하기
아래 코드는 위에 있는 코드를 express를 활용해서 구현한 코드입니다.
<br />

```js
const express = require('express') // 모듈을 불러온다.
const app = express(); // 모듈을 app담아 서버를 만듭니다!
const cors = require('cors') // cors 미들웨어를 불러온다.
const port = 5000;
const ip = 'localhost';
 
//우리가 구현해야될 파일을 불러 오기!!
app.use(express.static('client'))
app.use(express.json({strict: false})); // primitive data type 도 parsing 해주도록 설정
app.use(cors()); // 모든 요청에 대해 CORS 를 허용한다.
 
 
//POST 
//upper 구현하기
app.post('/upper', function(req,res){
    res.json(req.body.toUpperCase())
})

//loewr 구현하기
app.post('/lower', function(req,res){
    res.json(req.body.toLowerCase())
})
 
app.listen(port, ()=>{
  console.log(`http server listen on ${ip}:${port}`);
})
```
<br />
확실히 express 프레임워크를 사용하는게 코드가 좀더 깔끔하고 가독성 좋게 로직을 구성할수 있었고 사용성이 편리하고 유용하다는 것을 알수 있습니다!