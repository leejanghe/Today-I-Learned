# Project_dev #.8 (10/13) 중간 점검

---

## 1. 오늘 내가 한 일

로그인, 회원가입, 로그아웃기능 최종 완료, 로딩중 구현

<br />

## 2. 내일 내가 할 일

계속 미룬 렌딩페이지 파트 2,3 최종 완료 및 전반적인 테스크 파악, 배포 계획


<br />

## 3. 숙지 내용 및 알게 된 내용

### 3-1. 로딩중 구현

로딩중을 구현하기 위해 app.js에서 준비(로딩)상태를 관리 해주 었고 useEffect를 활용해서 비동기적으로 처리 하였습니다. 즉 로딩화면이 진행 되고 나서 메인 화면이 나올 수 있도록 하였고 삼항연산자를 사용해서 구현하였습니다.

```js
// 생략
const [ready, setReady] = useState(true)

useEffect(()=>{
    setTimeout(()=>{
      setReady(false)
    },3000)
  },[])

return ready?<Loading />:(이하 생략)
```

<br />

![로딩중](https://user-images.githubusercontent.com/75570030/137005781-a8d09c5b-cef1-4087-9446-bbdfb18211c0.gif)

<br />

### 3-2. 로그인 및 회원가입 창

기본적으로 그냥 쌩 css로 구현하였고 버튼에서 `<Link>`를 활용해서 로그인에서 회원가입으로 회원가입에서 로그인으로 갈 수 있도록 구현하였습니다.

<br />

![로그인,회원가입 창](https://user-images.githubusercontent.com/75570030/137005810-1ca3e483-ffa6-4d8d-b4b8-4b27eb33ade2.gif)

<br />

### 3-3. 로그인시 헤더 변화

우선 app.js에서 유저정보와 로그아웃, 로그인 관련 함수를 만들었고 그함수를 상태 끌어 올리기를 통해 프롭스로 전달 하였습니다. 그릐고 아래와 같이 유저의 정보를 받을떄와 아닐떄를 구분지어 렌더링이 될 수 있도록 하였습니다.

```js
// 생략
function Header({ userinfo, handleLogout }) {

    if(userinfo) {
        return (
          <div>
            <div className="header-background">
            <div className="header-container">
            <Link to="/" className="logo"><img src={logo} alt="logo"/></Link>
            <div className="grow"></div>
            <Link to="/UrlPage" className="header-flex-box">Url Service</Link>
              <div className="header-flex-box">Wellcome! {userinfo.username} 님</div>
              <div className="header-flex-box-logout" onClick={handleLogout}>Logout</div>
            </div>
          </div>
          </div>
        );
      } else {
        return (
          <div>
              <div className="header-background">
            <div className="header-container">
            <Link to="/" className="logo"><img src={logo} alt="logo"/></Link>
            <div className="grow"></div>
            <Link to="/LogIn" className="header-flex-box">Log in</Link>
            <Link to="/SignUp" className="header-flex-box">Sign Up</Link>
            </div>
            </div>
          </div>
        )
      }
    }

export default Header
```

<br />

![로그인시 헤더 변화](https://user-images.githubusercontent.com/75570030/137005828-d77da413-cd0b-45de-b67c-ae30fb072c9f.gif)

<br />

### 3-4. 로그아웃시 렌딩페이지로 전환

app.js에서 로그아웃 클릭시 아래와 같이 요청할수 있도록 설정하였고 useHistory를 활용해서 / 경로로 갈 수 있도록 설정 하였습니다!

```js
//생략
 const handleLogout = () => {
   axios
     .post('https://localhost:4000/logout')
     .then(() => {
       setUserinfo(null);
       setIsLogin(false);
       history.push('/');
     });
 };
```

<br />

![로그아웃시 헤더 변화](https://user-images.githubusercontent.com/75570030/137005838-6083766c-5494-46e2-8499-7893e1a3b6cd.gif)