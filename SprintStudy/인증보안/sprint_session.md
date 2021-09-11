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

