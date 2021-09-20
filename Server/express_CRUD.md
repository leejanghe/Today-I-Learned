# CRUD 트윗 로직

---

## tweet.js

```js
import express from "express";
import "express-async-errors";


let tweets = [
    {
        id: '1',
        text:"안뇽하세염!!",
        createdAt: Date.now().toString(),
        name:'Bob',
        username:'bob',
        url:''
    },
    {
        id: '2',
        text:"머하냠ㅋㅋㅋ 일 하세염!!",
        createdAt: Date.now().toString(),
        name:'joy',
        username:'joy',
        url:''
    }
]

const router = express.Router();

// get /tweets
// get /tweets?username=:username
router.get('/', (req,res,next)=>{
    const username = req.query.username;
    const data = username 
    ? tweets.filter(t=>t.username === username)
    : tweets;
    res.status(200).json(data)
    console.log(req.query)
})


// get /tweets/:id
router.get('/:id',(req,res,next)=>{
    console.log(req.params)
    const id = req.params.id;
    const tweet = tweets.find(t=> t.id === id);

    if(tweet){
        res.status(200).json(tweet)
    }else{
        res.sendStatus(404).json({meessage: `Twweet id(${id}) not found`})
    }
})

//post / tweets
router.post('/',(req,res,next)=>{
    const {text, name, username} = req.body;
    const tweet ={
        id: Date.now().toString(),
        text,
        createdAt:new Date(),
        name,
        username,
    };
    tweets = [tweet, ...tweets];
    res.status(201).json(tweet)
})


//put / tweets/:id
router.put('/:id',(req,res,next)=>{
    const id = req.params.id;
    const text = req.body.text;
    const tweet = tweets.find(t=>t.id === id);

    if(tweet){
        tweet.text = text;
        res.status(200).json(tweet)
    }else{
        res.sendStatus(404).json({meessage: `Twweet id(${id}) not found`})
    }
})


// delete / tweets/:id
router.delete('/:id',(req,res,next)=>{
    const id = req.params.id;
    tweets = tweets.filter(t => t.id !==id);
})



export default router;
```

<br />

## app.js

```js
import express from "express"
import cors from "cors"
import morgan from 'morgan' 
import helmet from 'helmet'
import "express-async-errors"

import tweetsRouter from './router/tweets.js'

const app = express(); 


app.use(express.json()) // 제이스 파싱
app.use(helmet()) // 보안에 도움
app.use(cors()) // 해더 셋팅 (다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여)
app.use(morgan('tiny'))  //로그 기록

app.use('/tweets', tweetsRouter); // 라우터 등록


app.use((req,res,next)=>{
    res.sendStatus(404)
})


app.use((error, req, res, next)=>{
    console.log(error)
    res.sendStatus(500)
})


app.listen(8080)
```