## nodemon 설치

노드몬사용하면 서버를 껐다 키기를 반복할 필요가 없습니다.

```js
npm i -g nodomon
```

<br />

## html 파일 전송하기

`sendfile()`함수를 쓰면 파일을 보낼 수 있습니다.    
`__dirname`은 현재 파일의 경로를 뜻합니다.  
`/` 하나만 있으면 홈페이지 홉입니다.  

```js
app.get('/',(req,res)=>{
    res.sendfile(__dirname + '/index.html')
})
```