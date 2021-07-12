## firebase

---

firebase는 벡앤드 기능을 클라우드 서비스 형태로 제공하기 때문에 서버리스 어플리케이션 개발이 가능합니다. 또한 모든 플랫폼을 프로젝트 구축시 자동으로 만들어 주며 프런트엔드에만 전념할 수 있습니다!
<br />


## firebase 실행

---

터미널에서 firebse를 추가합니다.

```js
npm add firebse
```
<br />

## firebase 초기설정

---

리엑트에서 서비스를 관리할 새로운 폴더를 하나 만들고 firebase 초기 설정 할 파일을 만듭니다.

```js
import firebase from "firebase";  
  
  const firebaseConfig = {
    apiKey: process.env.REACT_APP_FIREBASE_API_KEY,
    authDomain: process.env.REACT_APP_FIREBASE_AUTH_DOMAIN,
    projectId: process.env.REACT_APP_FIREBASE_PROJECT_ID,
    databaseURL: process.env.REACT_APP_FIREBASE_DB_URL,
  };
  // Initialize Firebase
const firebaseApp =  firebase.initializeApp(firebaseConfig);

export default firebaseApp;
```

초기설정할때 firebase에서 SDK를 가져와서 복붙합니다. 그리고 API키 보안을 위해 .evn파일을 만들어서 따로 관리해줍니다.
<br />

## firebase 로그인서비스 관리

---

로그인 서비스를 관리해주는 클래스 객체를 만들어 주고 아래와 같은 형식으로 작성합니다.

```js
import firebase from 'firebase';
import firebaseApp from './firebase';

class AuthService {
    login(providerName){
        const authPorvider = new firebase.auth[`${providerName}AuthProvider`]();
        return firebaseApp.auth().signInWithPopup(authPorvider);
    }
}

export default AuthService
```

## index.js 

---

index.js에 가서 변수를 하나 만들어 전에 만들었던 클래스 객체를 담아주고 앱에 전달합니다.

```js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.module.css';
import App from './app';
import AuthService from './service/auth_service';


const authService = new AuthService();
ReactDOM.render(
  <React.StrictMode>
    <App authService={authService}/>
  </React.StrictMode>,
  document.getElementById('root')
);
```

## app.js 

---

전달받은 프롭스를 로그인 컴포넌트에 전달합니다.

```js
import './app.css';
import Login from './components/login/login';

function App({authService}) {
  return (
   <Login authService={authService}/>
  );
}

export default App;
```

## Login 

---

전달받은 authService를 아래와 같이 로그인 서비스를 구현합니다.

```js
import React from 'react';
import Headers from '../header/header';
import Footer from '../footer/footer';

const Login = ({authService}) => {
    const onLogin = event => {;
        authService //
        .login(event.currentTarget.textContent)
        .then(console.log)
    };
        return(
            <section>
                <Headers />
                <section>
                    <h1>Login</h1>
                    <ul>
                        <li>
                            <button onClick={onLogin}>Google</button>
                        </li>
                        <li>
                            <button onClick={onLogin}>Github</button>
                        </li>
                    </ul>
                </section>
                <Footer />
            </section>
        );
    };

export default Login;
```