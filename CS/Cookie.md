## cookie

쿠키는 서버에서 클라이언트에 데이터를 저장하는 하나의 방법입니다. 서버가 원한다면 서버는 클라이언트에서 쿠키를 이용하여 데이터를 가져올 수 있습니다. 단순히 서버에서 클라이언트에 쿠키를 전송하는 것만 의미하지 않고 클라이언트에서 서버로 쿠키를 전송하는 것도 포합됩니다.<br >

### 서버가 클라이언트에 데이터를 저장할 수 있습니다.

무조건 데이터를 저장한 이후 아무 떄나 데이터를 가져올 수 없습니다. 데이터를 저장한 이후 특정 조건들이 만족하는 경우메나 다시 가져올 수 있습니다. 이러한 조건들은 쿠키 옵션으로 표현할수 있습니다.

<br />

## 쿠키 옵션

### 1. Domain

도메인은 쉽게 말해 `www.naver.com`과 같은 서버에 접속할 수 있는 이름입니다. 쿠키옵션에서의 도메인은 포트, 세부 경로, 정보 및 서브 도메인을 포함하지 않습니다. 서브도메인인 `www.`가 빠진 `naver.com`이 됩니다. 만약 쿠키 옵션에서 도메인 정보가 존재한다면 클라이언트에서는 쿠키의 도메인 옵션과 서버의 도메인이 일치해야만 쿠키를 전송할 수 있습니다.

<br />

### 2. Path

서버가 라우팅할 때 사용하는 경로입니다. 만약 요쳥해야할 URL이 `http://www.localhost.com/users.login`인 경우라면 Path, 세부 경로는 `/users/login`이 됩니다. 명시하지 않을경우 기본으로 `/`으로 설정 되어 있습니다. 쿠키를 전송하기 위해선 쿠키옵션의 Path와 요청 경로가 일치해야 가능합니다. <br />

```js
//쿠키전송 가능한 경우
/user           //Path옵션
// 요청경로
/user/login

//쿠키전송 불가능한 경우
/user           //Path옵션
// 요청경로
/users/login    // Path옵션을 만족하지 못해 쿠키 전송  x
```

<br />

## Secure

쿠키를 전송해야 할 때 사용하는 프로토콜에 따른 쿠키 전송 여부를 결정합니다. 만약 해당 옵션이 true로 설정된 경우, HTTPS 프로토콜을 이용하여 통신하는 경우에만 쿠키를 전송할 수 있습니다. (http는 secure속성으로 쿠키를 설정할수 없습니다.) 

<br />

## HttpOnly

자바스크립트에서 브라우저의 쿠키에 접근 여부를 결정합니다. 만약 해당 옵션이 true로 설정된 경우, 자바스크립트에서 쿠키에 접근이 불가합니다. 명시되지 않는 경우 기본으로 false로 지정되어 있습니다. (false인경우 쿠키 접근이 가능해 XSS공격에 취약)

<br />

## MaxAge or Expires

쿠키가 유효한 기간을 정하는 옵션입니다. MaxAge는 몇 초 동안 쿠키가 유효한지 설정하는 것이고 Expires는 클라이언트 기준으로 Date를 지정합니다. 시간 날짜를 초과하면 쿠키는 자동으로 파괴됩니다. 하지만 두옵션을 지정하지 않을 경우 브라우저의 탭을 닫아야만 쿠키가 제거될 수 있습니다.

<br />

## SameSite

Cross-Origin 요청을 받은 경우 요청에서 사용한 메소드와 해당 옵션의 조합으로 서버의 쿠키 전송 여부를 결정합니다.

### Lax

사이트가 서로 달라도, GET 요청이라면 쿠키 전송이 가능합니다.

### Strict

사이트가 서로 다르면, 쿠키 전송을 할 수 없으며 Cross-Origin이 아닌 same-site인 경우에만 쿠키를 전송 할수 있습니다.

### None
사이트가 달라도, 모든(GET, POST, PUT 등등) 요청에 대해 쿠키 전송이 가능하다. 다만 쿠키 옵션 중 Secure 옵션이 필요합니다.

<br />

이때 'same-site'는 요청을 보낸 Origin과 서버의 도메인이 같은 경우를 말합니다. 이러한 옵션들을 지정한 다음 서버에서 클라이언트로 쿠키를 처음 전송하게 된다면 헤더에 Set-Cookie라는 프로퍼티에 쿠키를 담아 쿠키를 전송하게 됩니다. 이후 클라이언트 혹은 서버에서 쿠키를 전송해야 한다면 클라이언트는 헤더에 Cookie라는 프로퍼티에 쿠키를 담아 서버에 쿠키를 전송하게 됩니다.

<br />

## cookie 설정 코드

express-session 라이브러리를 이용해 쿠키 설정을 해줄 수 있습니다.

```js
//...생략

app.use(
  session({
    secret: '@codestates',
    resave: false,
    saveUninitialized: true,

    // 쿠키 설정
    cookie: {
      domain: 'localhost',
      path: '/',
      maxAge: 24 * 6 * 60 * 10000,
      sameSite: 'None',
      httpOnly: true,
      secure: true,
    },
  })
);

//...생략
```

<br />

## 쿠키 옵션 Point 정리

domain - 서버와 요청의 도메인이 일치하는 경우 쿠키 전송  
path - 서버의 요청의 세부경로가 일치하는 경우 쿠키 전송  
maxage/expires - 쿠키의 유효기간 설정  
httpOnly - 스크립트의 쿠키 접근 가능 여부 설정  
secure - HTTPS 에서만 쿠키 전송 여부 설정  
sameSite - 같은 사이트에서만 쿠키를 사용할 수 있게 하는 설정  