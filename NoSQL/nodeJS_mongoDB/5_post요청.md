## POST요청하기

간단한 예시를 통해 post 요청하기

```js
<div class="container mt-3">
  <form action="/add" method="POST">
    <div class="form-group">
      <label>오늘의 할일</label>
      <input type="text" class="form-control" name="title">
    </div>
    <div class="form-group">
      <label>날짜</label>
      <input type="text" class="form-control" name="date">
    </div>
    <button type="submit" class="btn btn-outline-secondary">Submit</button>
  </form>
</div>
```

폼 전성버튼을 누를시 /add 라는 경로로 POST 요청을 합니다.  
form 태그의 method속성은 GET/POST 중 어떤 요청을 할 건지 정해주는 부분,  
action은 어떤 경로로 요청할건지 정해주는 부분입니다.  

중요포인트 input에 name 속성을 이용해서 어떤 데이터인지 확인해줄수 있습니다.(req.body)

<br />

## body-parser 설치 x

2021년 이후로 설치한 프로젝트들은 body-parser 라이브러리가 express에 기본 포함이라 따로 npm 설치할 필요가 없습니다!  

```js
// 그냥 이거 쓰기 바디값을 가져온다라고 이해하기
app.use(express.urlencoded({extended:true}))
```

<br />

## 요청 데이터 가져오기

req.body를 출력하면 객체안에 데이터를 확인할수 있습니다.


```js
app.use(express.urlencoded({extended:true}))
//app.use(express.json({strict:false}))

app.get('/',(req,res)=>{
    res.sendfile(__dirname + '/index.html')
})

app.get('/write',(req,res)=>{
    res.sendfile(__dirname + '/write.html')
})

app.post('/add',(req,res)=>{
    res.send('전송완료')
    console.log(req.body.title)
    console.log(req.body.date)
})
```