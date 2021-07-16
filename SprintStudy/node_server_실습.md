# nodo server 실습하기
mini node server 스프린트를 통해 실습해보는 시간을 갖겠습니다!
<br />

## upper / lower server 구현하기
이번 스프린트는 서버를 구현하기 위한 6단계 방법과 코드 내용을 정리해 보겠습니다!(자잘한거는 생략하고 createServer부분만 징행 하겠습니다.)

---

## 1단계 요청 메서드 정리 하기
1단계는 크게 "POST"와 "OPTION" 이 두가지 요청 메서드로 구간을 나눠 줍니다!
<br /> 

```js
const server = http.createServer((request, response) => {
if(request.method === "POST"){

}

if(request.method === "OPTION"){

}
});
```
<br /> 

## 2단계 라우터 정의 하기
2단계는 url주소가 lower인 경우와 upper인 경우로 라우터를 정의 합니다!
<br /> 

```js
const server = http.createServer((request, response) => {
if(request.method === "POST"){
    if(request.url === '/lower'){


    }else
    if(request.url === '/upper'){


    }
}

if(request.method === "OPTION"){

}
});
```
<br />

## 3단계 요청 데이터 받기
3단계는 request.on 활용해서 데이터를 받아 옵니다.
<br /> 

```js
const server = http.createServer((request, response) => {
if(request.method === "POST"){
    if(request.url === '/lower'){
    let data = ''
    
    request.on('data',(chunk)=>{ //on은 어떤 이벤트를 줄경우 콜백함수를 그에 맞춰 실행하는 메서드 입니다.
    data = data + chunk        //청크를 통해 바디값을 받아올 수 있습니다.(단 on이라는 데이터 키워드를 넣어야 됨)
    })

    request.on('end',()=>{ //data와 end는 약속된 키워드 이벤트 입니다.
    data
    })

    }else
    if(request.url === '/upper'){


    }


if(request.method === "OPTION"){

}
});
```
<br />

## 4단계 동작 구현하기!
4단계는 우리가 구현할 대문자 소문자로 변환해주는 메서드를 활용해서 구현하면 됩니다. 
<br /> 

```js
const server = http.createServer((request, response) => {
if(request.method === "POST"){
    if(request.url === '/lower'){
    let data = ''
    
    request.on('data',(chunk)=>{
    data = data + chunk        
    })
    request.on('end',()=>{ 
    data = data.toUpperCase() // 4단계 동작 구현
    })

    }else
    if(request.url === '/upper'){


    }
}

if(request.method === "OPTION"){

}
})
```
<br />

## 5단계 데이터 상태 응답하기
5단계는 response.writehead와 end를 써서 응답하면 됩니다! 여기까지 한것을 upper에 복사 붙이기를 하고 구현단계에서 toUpperCase()로 바꿔 주면 됩니다!
<br /> 

```js
const server = http.createServer((request, response) => {
if(request.method === "POST"){
    if(request.url === '/lower'){
    let data = ''
   
    request.on('data',(chunk)=>{
    data = data + chunk        
    })
    request.on('end',()=>{ 
    data = data.toUpperCase() // 4단계 동작 구현
    //5단계 상태 응답하기
    response.writeHead(201, defaultCorsHeader); //상태 코드와 cors 응답
    response.end(data) // end는 응답하기 위한 메서드 (데이터 전달)
    })

    }else
    if(request.url === '/upper'){
    let data = ''
   
    request.on('data',(chunk)=>{
    data = data + chunk        
    })
    request.on('end',()=>{ 
    data = data.toLowerCase() // 4단계 동작 구현
    //5단계 상태 응답하기
    response.writeHead(201, defaultCorsHeader); //상태 코드와 cors 응답
    response.end(data) // end는 응답하기 위한 메서드 (데이터 전달)
    })

    }


if(request.method === "OPTION"){
    response.writeHead(201, defaultCorsHeader); //상태 코드와 cors 응답
    response.end(data) // end는 응답하기 위한 메서드 (데이터 전달)
}
})
```
<br />

## 6단계 에러 처리하기
6단계는 5단계 형식과 같이 에러처리를 하면 됩니다. (404 상태에러처리)
<br /> 

```js
//...셍략
if(request.url === '/upper'){
    let data = ''
   
    request.on('data',(chunk)=>{
    data = data + chunk        
    })
    request.on('end',()=>{ 
    data = data.toLowerCase() // 4단계 동작 구현
    //5단계 상태 응답하기
    response.writeHead(201, defaultCorsHeader); //상태 코드와 cors 응답
    response.end(data) // end는 응답하기 위한 메서드 (데이터 전달)
    })
    //6단계 에러처리
    }else{
    response.writeHead(404, defaultCorsHeader); //상태 코드와 cors 응답
    response.end("Not found 404") // end는 응답하기 위한 메서드 (데이터 전달)
    }


if(request.method === "OPTION"){
    response.writeHead(201, defaultCorsHeader); //상태 코드와 cors 응답
    response.end(data) // end는 응답하기 위한 메서드 (데이터 전달)
}
})
   
```
<br />

## 최종코드 정리

---

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