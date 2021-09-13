# 세션 스프린트

---

# 기본설정

## 1. 환경변수 설정

기본 설정은 세션스프린트에 나와있기 때문에 생략!

<br />

# Server

## 1. https 인증서 가져오기

```
$ mkcert -key-file key.pem -cert-file cert.pem localhost 127.0.0.1 ::1
```

위와 같이 사설 인증서를 발급하면 개인키 공개키 파일이 생성됩니다.

<br />

## 2. index.js 임폴트값 변경

무슨의도로 임폴트를 다르게 했는지 모르겠지만 httpsServer를 server로 변수를 변경합니다. 그래야 import 할수 있습니다.

<br />

## 3. controller (login)

```js
const { Users } = require('../../models');
const jwt = require('jsonwebtoken');

module.exports = async(req, res) => {
  // TODO: urclass의 가이드를 참고하여 POST /login 구현에 필요한 로직을 작성하세요.

  const userInfo = await Users.findOne({
    where:{userId: req.body.userId, password:req.body.password}
  })

  // 일치하지 않은 유저가 존재 할경우
  if(!userInfo) return res.status(400).json({data:null, message:"not authorized"})

  // 일치하는 유저가 존재할 경우
  // accessToken과 refreshToken 생성

  const {id,userId,email,createdAt,updatedAt} = userInfo; //payload라 생각하기
  
  const accessToken = jwt.sign({id,userId,email,createdAt,updatedAt}, process.env.ACCESS_SECRET, { expiresIn: '2h'});
  const refreshToken = jwt.sign({id,userId,email,createdAt,updatedAt}, process.env.REFRESH_SECRET, { expiresIn: '12h'});

  //console.log('@@@@@@@@@@@@@@@@@@@@@@@@@',accessToken)

  //성생된 refreshToken 쿠키에 담아줌
  res.cookie('refreshToken', refreshToken, { SameSite:'none',httpOnly: true, secure: true });
  res.status(200).json({data:{accessToken:accessToken},message:"ok"})
};
```

1. DB정보를 findOne메서드를 활용해서 조회합니다. 
2. 유저가 존재하지 않을 경우와 존재하는 경우를 생각해서 로직을 작성합니다.
3. 유저가 존재한다면 access / refresh 토큰을 등록해줍니다. 등록 해줄때 `const jwt = require('jsonwebtoken');`해서 라이브러리를 사용합니다. 
- sign은 jwt를 등록해주는 함수입니다. jwt.sign(토큰에 담아줄값,access_secret,{옵션})
4. 리프레쉬 토큰은 쿠키에 담아 보내줍니다.
- cookie('이름명',리프레쉬토큰,{쿠키설정})

<br />

## 4. controller (assecss token)

```js
const { Users } = require("../../models");
const jwt = require("jsonwebtoken");

module.exports = async (req, res) => {
  // TODO: urclass의 가이드를 참고하여 GET /accesstokenrequest 구현에 필요한 로직을 작성하세요.
  const authorization = req.headers.authorization;

  // authorization header에 토큰이 담겨져 있지 않은 경우
  if (!authorization) return res.status(400).json({ data: null, message: "invalid access token" });
  
  const token = authorization.split(" ")[1];

  // accessToken이 유효한지와 서버에서 가지고 있는 키로 생성한 것인지 확인
  const data = jwt.verify(token, process.env.ACCESS_SECRET, {}, (err, res) => {
    if (err) return err.message;
    else return res;
  });

  console.log("dataad입니다",data)

  // 복호화할 수 없거나 유효하지 않은 토큰일 경우
  if (!data) return res.status(400).json({ data: null, message: "invalid access token" });

  // jwt 복호화 데이터로 DB의 Users 테이블 조회
  const userInfo = await Users.findOne({ where: { userId: data.userId } });
  console.log("@@@@@@@@@",userInfo)
  // 일치하는 유저가 존재하지 않을 경우
  if (!userInfo)
    return res.status(400).json({ data: null, message: "access token has been tempered" });

  // 일치하는 유저가 존재할 경우
  const { id, userId, email, createdAt, updatedAt } = userInfo;
  res.json({ data: { userInfo: { id, userId, email, createdAt, updatedAt } }, message: "ok" });
};
```

1. 콘솔로 req.headers 치면 토큰이 담겨져있는 것을 확인할수 있습니다.
2. 헤더에 있는 토큰을 스플릿 하여 토큰만 가져올수 있도록 변수를 지정합니다.
3. 가져온 토큰을 verify함수를 활용해서 유효성 검사를 진행합니다.
4. jwt 복호화 데이터로 db정보를 조회하고 그중에서 일치하거나 일치 않을 때 로직을 작성합니다.

<br />

## 5. controller (refresh assecsstoken)

```js
const { Users } = require('../../models');
const jwt = require('jsonwebtoken');

module.exports = (req, res) => {
  // TODO: urclass의 가이드를 참고하여 GET /refreshtokenrequest 구현에 필요한 로직을 작성하세요.
  //console.log('@@#!@#!@#!@#!@#!@#!@#',req.cookies)

  const refreshToken = req.cookies.refreshToken
  //console.log('리프레쉬 토큰가져오기',req.cookies)
  //console.log('@#!@#!@#!@#',refreshToken)
  console.log("@@@@#!@#!@#!@#",refreshToken)
  const data = jwt.verify(refreshToken, process.env.ACCESS_SECRET,(err,resdata)=>{
    if(err) return err
    return resdata
    
});
//console.log('@@@@@@@@@@@@@@',data)

// 쿠키에 리프레쉬 토큰이 없는 경우
if(!refreshToken) 
return res.status(400).json({data:null, message:'refresh token not provided'})

// 유요하지 않은 리프레쉬 토큰을 전달 받은 경우
if(refreshToken === "invalidtoken") 
return res.status(400).json({data:null, message:'invalid refresh token, please log in again'})


const accessToken = jwt.sign(data, process.env.ACCESS_SECRET);
delete data.iat
res.status(200).json({data:{accessToken,userInfo:data},message:"ok"})
}
```

1. 중요포인트는 쿠키에 로그인서버에서 만들었던 리프레쉬 토큰이 담겨있는지 확인하는 작업이 필요합니다.
- 확인방법은 콘솔로 req.cookies 쳐서 확인합니다. 안에 리프레쉬 토큰이 담겨있습니다.
2. 리프레쉬 토큰도 유효검사를 하고 토큰이 유효한경우와 없는경우의 로직을 작성합니다.
3. 일치하는 유저가 있으면 테이터를 담아 보내줍니다.

<br />

# Client

클라이언트 설명은 이미 세션에서 많이 했기때문에 참고 하기

## 1. login page

```js
//...생략
async loginRequestHandler() {
    /*
    TODO: Login 컴포넌트가 가지고 있는 state를 이용해 로그인을 구현합니다.
    로그인을 담당하는 api endpoint에 요청을 보내고, 받은 데이터로 상위 컴포넌트 App의 state를 변경하세요.
    초기 App:
    state = { isLogin: false, accessToken: "" }
    로그인 요청 후 App:
    state = { isLogin: true, accessToken: 서버에_요청하여_받은_access_token }
    */
    const url = 'https://localhost:4000/login'
    const {userId, password} = this.state

    let res = await axios.post(url, {userId, password},{withCredentials:true})


    //console.log('@@@#@#!#!@#!@#!@#',res.data)
    this.props.loginHandler(res.data.data.accessToken);
    
  }
  //...생략
```

<br />

## 1. my page

```js
//... 생략
 async accessTokenRequest() {
    /* 
    TODO: 상위 컴포넌트인 App에서 받은 props를 이용해 accessTokenRequest 메소드를 구현합니다.
    access token을 처리할 수 있는 api endpoint에 요청을 보내고, 받은 데이터로 Mypage 컴포넌트의 state (userId, email, createdAt)를 변경하세요
    초기 Mypage:
    state = { userId: "", email: "", createdAt: "" }
    accessTokenRequest 후 Mypage:
    state = { userId: "특정유저id", email: "특정유저email", created: "특정유저createdAt" }
    
    ** 주의사항 **
    App 컴포넌트에서 내려받은 accessToken props를 authorization header에 담아 요청을 보내야 합니다. 
    */
   const url = "https://localhost:4000/accesstokenrequest"
   const res = await axios.get(url, 
    {headers:{Authorization:"Bearer "+this.props.accessToken}},{withCredentials: true})

    console.log('@@@@@@##@#!!$!@#',res.data)
    if(res.data.data){
      const { createdAt, userId, email } = res.data.data.userInfo
      this.setState({createdAt, userId, email})
    }
  }

    async refreshTokenRequest() {
    /*
    TODO: 쿠키에 담겨져 있는 refreshToken을 이용하여 refreshTokenRequest 메소드를 구현합니다.
    refresh token을 처리할 수 있는 api endpoint에 요청을 보내고, 받은 데이터로 2가지를 구현합니다.
    1. Mypage 컴포넌트의 state(userId, email, createdAt)를 변경
    2. 상위 컴포넌트 App의 state에 accessToken을 받은 새 토큰으로 교환
    */
    const refreshTokenUrl = "https://localhost:4000/refreshtokenrequest"
    const res = await axios.get(refreshTokenUrl,{withCredentials: true})
    console.log(res.data)
    if(res.data.data !== undefined){
      const { createdAt, userId, email } = res.data.data.userInfo
      this.setState({createdAt, userId, email})
    }
    this.props.issueAccessToken(res.data.data.accessToken);
  }
  //...생략
```