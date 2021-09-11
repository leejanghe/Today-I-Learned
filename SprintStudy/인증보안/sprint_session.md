# 세션 스프린트

---

# 기본설정

## 1. 환경변수 설정

우선 env파일 이름을 수정하고 데이터 베이스에 연결할수 있도록 설정한다. 

<br />

## 2. 데이터 베이스 마이그레이션

```
npx sequelize-cli db:migrate
```

이번스프린트에선 시퀄라이즈와 모델 생성까지 완료되어 있어서 마이그레이션, 시드만 진행하면 됩니다.

<br />

## 3. 데이터 베이스 연결 확인

마이그레이션 후 npm test를 통해 데이터베이스가 잘연결되었는지 확인합니다.

<br />

# Server

## 1. https 인증서 가져오기

```
$ mkcert -key-file key.pem -cert-file cert.pem localhost 127.0.0.1 ::1
```

위와 같이 사설 인증서를 발급하면 개인키 공개키 파일이 생성됩니다.

<br />

## 2. index.js cors와 session 옵션 설정

```js
// TODO: express-session 라이브러리를 이용해 쿠키 설정을 해줄 수 있습니다.
app.use(
  session({
    secret: '@codestates',
    resave: false,
    saveUninitialized: true,
    cookie: {
      domain: 'localhost', //도메인 설정
      path: '/',  // 경로
      maxAge: 24 * 6 * 60 * 10000, // 쿠키 유효 기간
      sameSite: 'None', //항상 쿠키를 보내주는 역할 (secure 옵션 필수)
      httpOnly: true, // 자바스크립트 접근 허용 안함 (XSS 공격 방지)
      secure: true,  // https 프로토콜을 이용할 경우 쿠키 전송
    },
  })
);
app.use(logger('dev'));
app.use(express.json());
app.use(express.urlencoded({ extended: false }));

// TODO: CORS 설정이 필요합니다. 클라이언트가 어떤 origin인지에 따라 달리 설정할 수 있습니다.
// 메서드는 GET, POST, OPTIONS를 허용합니다.

const options ={
  origin:'https://localhost:3000',
  methods:['GET','POST','OPTION'],
  credentials:true
}

app.use(cors(options));
```

express에서는 세션쿠키를 사용할수 있도록 라이브러리가 내장되어있습니다. 설치하면 위와 같이 세션 쿠키 객체 안에 옵션을 설정할수 있습니다. 쿠키 옵션은 주석을 참고하기 두번째 cors설정에서 credentials은 쿠키를 보낼때 꼭 써야하는 옵션입니다.  

중요포인트  
HTTP Cookie와 HTTP Authentication 정보를 인식할 수 있게 해주는 요청이다. 클라이언트는 요청 생성 시 반드시 withCredentials = true;로 지정해주어야 한다.

<br />

## 3. controller 서버 구현(login)

```js
const { Users } = require('../../models');

module.exports = {
  post: async (req, res) => {
    // userInfo는 유저정보가 데이터베이스에 존재하고, 완벽히 일치하는 경우에만 데이터가 존재합니다.
    // 만약 userInfo가 NULL 혹은 빈 객체라면 전달받은 유저정보가 데이터베이스에 존재하는지 확인해 보세요
    const userInfo = await Users.findOne({
      where: { userId: req.body.userId, password: req.body.password },
    });
    console.log(req.body) //{ userId: 'kimcoding', password: '1234' }
    console.log(userInfo) // 유저정보 다출력
  
    // TODO: userInfo 결과 존재 여부에 따라 응답을 구현하세요.
    // 결과가 존재하는 경우 세션 객체에 userId가 저장되어야 합니다.
    if (!userInfo) {
      // your code here
      res.status(400).send({data:null,message: "not authorized"});
    } else {
      // your code here
      // HINT: req.session을 사용하세요.
      req.session.sid = userInfo.userId; 
      res.status(200).send({data:userInfo,message: "ok"})
      console.log(req.session.sid)  // kimcoding
    }
  }
}
```

로그인 서버에서 중요한 포인트는 findOne메서드를 활용해서 디비 정보를 조회하는 것이다. 로그인을 할때는 아이디와 비밀번호를 가져오는 작업을 한다. 두번째로 중요한 포인트는 세션객체 아이디에 유저정보의 아이디를 넣어 주는 작업을 하는 것이다. 넣어주는 방법은 req.session.sid를 활용하면 된다. (sid대신 userId를 해도 된다. sid는 세션id란 뜻으로 통상적으로 많이 쓴다.)

<br />

## 4. controller 서버 구현(logout)

```js
module.exports = {
  post: (req, res) => {

    // TODO: 세션 아이디를 통해 고유한 세션 객체에 접근할 수 있습니다.
    // 앞서 로그인시 세션 객체에 저장했던 값이 존재할 경우, 이미 로그인한 상태로 판단할 수 있습니다.
    // 세션 객체에 담긴 값의 존재 여부에 따라 응답을 구현하세요.
    console.log("--------",req.session) // 세션객체와 세션아이디가 출력된다.
    if (!req.session.sid) {
      // your code here
      res.status(400).send({data:null, "message":"not authorized"})
    } else {
      // your code here
      // TODO: 로그아웃 요청은 세션을 삭제하는 과정을 포함해야 합니다.
      
      //req.session.sid = '';
      req.session.destroy(); // 아이디 삭제하는 방법
      res.status(200).send({data:null,"message":"ok"})
    }
  },
};
```

로그아웃의 핵심은 세션객체 안에 있는 아이디를 삭제하는 것이다. 세션 아이디를 삭제하는 방법은 req.session.destroy()를 사용하면 된다. 혹은 빈문자열로 넣어도 상관 없습니다.

<br />

## 5. controller 서버 구현(userinfo)

```js
const { Users } = require('../../models');

module.exports = {
  get: async (req, res) => {

    // TODO: 세션 객체에 담긴 값의 존재 여부에 따라 응답을 구현하세요.
    // HINT: 세션 객체에 담긴 정보가 궁금하다면 req.session을 콘솔로 출력해보세요

    console.log('@@@@@@@@@@@@@@@@@@@@@@',req.session.sid) // 세션객체 안에 kimcoding
    if (!req.session.sid) {
      // your code here
      res.status(400).json({"message":"not authorized"})
    } else {
      // your code here
      // TODO: 데이터베이스에서 로그인한 사용자의 정보를 조회한 후 응답합니다.
      const userInfo = await Users.findOne({
        where: { userId: req.session.sid},
      });
      console.log(userInfo) //세션객체 안에 유저 정보가 담겨 있습니다.
        res.status(200).json({"data":userInfo,"message":"ok"})
    }
  },
};
```

유저인포 부분은 세션객체에 있는 아이디를 잘 활용해서 로직을 작성하면 됩니다. 세션객체에 유저에 대한 정보가 다있기때문에 아이디만 조회해서 로직을 작성하면 됩니다.

<br />

# Client

## 1. login page

```js
//...생략

 loginRequestHandler() {
    // TODO: 로그인 요청을 보내세요.
    //
    // 로그인에 성공하면
    // - props로 전달받은 함수를 호출해, 로그인 상태를 변경하세요.
    // - GET /users/userinfo 를 통해 사용자 정보를 요청하세요
    //
    // 사용자 정보를 받아온 후
    // - props로 전달받은 함수를 호출해, 사용자 정보를 변경하세요.
    let logInUrl = 'https://localhost:4000/users/login'
    let userInfo = 'https://localhost:4000/users/userinfo'

    console.log(this.state.username)
    axios.post(logInUrl,{
      userId:this.state.username,
      password:this.state.password
    },{'Content-Type':'application/json',withCredentials:true})
    .then(res=>this.props.loginHandler())
    .then(res=>axios.get(userInfo,{withCredentials:true}).then(res=> this.props.setUserInfo(
      res.data.data
    )))
    .catch(err=>console.log('err'))
  }

  //...생략
  ```

로그인 페이지의 핵심은 로그인이 된 후 바로 유저 정보를 받아와서 마이페이지로 들어갈수 있도록 로직을 작성해야 합니다. 그래서 로그인을 할때 로그인서버에 요청하여 로그인상태를 변경하고 사용자의 정보를 get요청해서 setUserInfo함수를 활용해서 유저의 상태정보를 변경할수 있도록 로직을 작성하면 됩니다. 여기서 중요한 점은 `withCredentials:true` 입니다. 이설정은 서버에서 cors에서 옵션을 `credentials:true`했으면 클라에서 무조건 해야되는 설정입니다. 이설정을 해야 쿠키가 잘 전송이 됩니다.

<br />

## 1. Mypage

```js
//...생략
function Mypage(props) {
  const handleLogout = () => {
    // TODO: 서버에 로그아웃 요청을 보낸다음 요청이 성공하면 props.logoutHandler를 호출하여 로그인 상태를 업데이트 해야 합니다.
    let logoutUrl = 'https://localhost:4000/users/logout'

    axios.post(logoutUrl,null,{'Content-Type':'application/json', withCredentials:true})
    .then(res=>props.logoutHandler())
    .catch(err=>console.log('err'))
  };

//...생략
```

로그아웃 페이지는 로그아웃을 구현한 서버를 불러와 요청하면 됩니다. 여기서 중요한 포인트는 axios를 사용할때 post와 get요청이 있는데 들어가는 인자가 다릅니다. post요청은(url, 정보, 옵션) 으로 3개가 들어가고 get요청은(url, 옵션)으로 2개가 들어갑니다. 이점만 유의해서 로직을 작성하면 됩니다.
