# Project_dev #.4 (10/12)

---

## 1. 오늘 내가 한 일

로그인 페이지, 회원가입 페이지 일부 서버에러 수정, KPT회고 작성, 렌딩페이지(2,3파트 추후수정) 머지, 로그인,회원가입 css정리

<br />

## 2. 내일 내가 할 일

렌딩페이지 파트 2,3마무리 머지 푸쉬, 로그인,회원가입 페이지 머지 푸쉬, 로그인 상태 아닐때 url페이지로 못가게 제한걸기


<br />

## 3. 숙지 내용 및 알게 된 내용

서버 권한에서 토큰 전달과정에서 베어를 받아 오지 않는데 스플릿을 주어서 에러가 걸렸다. 또한 req.cookies로 쿠키에 있는 내용들을 다받을 수 있게 된다는 것을 알게 되었다. 굳이 req.cookie.header를 할필요가 없었다.

```js
isAuthorized: (req) => {


    // req.cookies => 쿠키에 있는 내용들 다 받을수 있음
    const authorization = req.cookies.accessToken
    console.log(authorization)
   
    if(!authorization) {
      return null;
    }

    //스필릿을 안하는 이유 위에서 베어럴을 안넣었기떄문에 스플릿 안해도된다.
    const userInfo = authorization
    try {
      return verify(userInfo, process.env.ACCESS_SECRET);
    } catch (err) {
      return null;
    }
  }
  ```


  ## 4. 느낌...

  2일 남았다... 1주일 안에 뭔가 만들기엔 너무 빠듯한 시간이였고 여유가 너무 없었다.. 그래도 뭔가 많이 한거 같아서 뿌듯한 느낌도 든다.. 4주차 때는 좀 더 확실하게 준비해서 진행해야 겠다.. 이번엔 너무 빈틈이 많았고 시간적 압박으로 집중을 많이 못했다... 후.. 남은 기간동안 그냥 밤세자... ㅋㅋㅋ