## POST 요청하기

아래와 같이 표현이 가능합니다.

```js
app.post('/add',(req,res)=>{
        res.send('전송완료')
        console.log(req.body.title)
        console.log(req.body.date)
   
    db.collection('post').insertOne({제목:req.body.title, 날짜:req.body.date},(err,result)=>{
        console.log('저장완료')
       })
    });
```

res.send()는 항상 존재해야 합니다. 전송이 실패하든 성공하든 뭔가 서버에 보내야 합니다. 안그러면 브라우저가 멈춥니다. 그래서 메세지 같은걸 보내주기 싫다면 간단한 응답코드나 리다이렉트(페이지강제이동)를 해주는 코드도 있습니다.

<br />

## ejs 사용하기 , ejs파일만들기

우선 터미널에 ejs를 설치합니다.

```js
npm install ejs
```

설치후 js상단에 ejs사용 세팅을 합니다.

```js
app.set('view engine','ejs'); // ejs 셋팅


  app.get('/list',(req,res)=>{
        res.render('list.ejs');
    })

```

그전에 주의할점!! 작업폴더 내에 views라는 이름의 폴더를 하나 만든후 거기에 ejs파일을 만들어야 합니다!

<br />

## ejs 사용법

```js
<%= 변수이름  %>
```