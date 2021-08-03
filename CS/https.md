## Https 프로토콜

https는 http 요청을 SSL혹은 TLS라는 알고리즘을 이용해 HTTP통신을 하는 과정에서 내용을 암호화하여 데이터를 전송하는 방법입니다. https는 http보다 상대적으로 안전한 방법이고, 데이터 제공자의 신원을 보장받을 수 있습니다.

<br />

## 암호화

HTTPS 프로토콜의 특징 중 하나는 암호화된 데이터를 주고 받기 때문에, 중간에 인터넷 요청이 탈취되더라도 복호화 하기 전까지는 그 내용을 알아볼 수 없습니다.

<br />

## 인증서

https 프로토콜의 또 다른 특징 중 하나는 브라우저가 응답과 함께 전달된 인증서 정보를 확인할 수 있습니다. 브라우저는 인증서에 해당 인증서를 발급한 CA 정보를 확인하고 인증된 CA가 발급한 인증서가 아니라면 경고창을 띄워 서버 연결이 안전하지 않다고 화면에 보여줍니다.

<br />

---

## HTTPS 사설 인증서 발급

moaOS 경우, homebrew통해 mkcert를 설치할 수 있습니다.

```js
$ brew i mkcert
$ brew i nss //firefox를 사용할 경우 이거 설치
```

## 인증서 생성

아래 명령어로 로컬을 인증된 발급기관으로 추가합니다.

```js
$ mkcert -i
```

아래코드는 로컬 환경에 대한 인증서를 만드는 코드입니다.

```js
$ mkcert -key-file key.pem -cert-file cert.pem localhost 127.0.0.1 ::1
```

위코드를 통해 `cert.pem`, `key.pem` 이라는 파일이 생성이 된 것을 확인할수 있습니다. `key.pem`의 경우 개인 키이므로 git 커밋이 아닌 환경변수를 활용해 암호처럼 다뤄야 합니다.

<br />


## https 서버 기본 구현 코드

```js
const https = require('https');
const fs = require('fs');
const express = require('express');

const app = express();

https
  .createServer(
    {
      key: fs.readFileSync(__dirname + '/key.pem', 'utf-8'),
      cert: fs.readFileSync(__dirname + '/cert.pem', 'utf-8'),
    },
    app.use('/', (req, res) => {
      res.send('Congrats! You made https server now :)');
    })
  )
  .listen(3001);
  ```