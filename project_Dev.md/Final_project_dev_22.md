# Final_Project_dev #.22 (11.10)

---

## 1. 여태 내가 한 일들 

- 마이페이지 회원정보, 찜목록 css 정리
- 마이페이지 회원정보 라우터 설정
- 메인 페이지 터치 css 정리

<br />

## 2. 내일 내가 할 일

- 마이페이지, 메인 페이지 최종 css 마무리

<br />

## 3. 에러 헨들링

Nothing was returned from render. This usually means a return statement is missing. Or, to render nothing, return null. 라는 에러 문구를 만나게 되었다. 인터넷 검색을 통해서 or 연산자를 사용해서 해결 하라고 했는데 해결 되지 않았다...아무리 생각해도 이문제는 undefined 보다는 렌더링 문제에 더 가까운 것 같다.. 우선 검색을 통해 본 레퍼런 스 들이다.

```js
// 원인 코드
import React from 'react';
import './App.css';

function App() {
  const name = undefined;
  return name;
}

export default App;
```

보통 다음과 같이 리액트 컴포넌트 함수에서 undefined를 반환하여 렌더링 하는 상황에서 발생한다.

```js
// 해결 코드
import React from 'react';
import './App.css';

function App() {
  const name = undefined;
  return name || '값이 undefined입니다.';
}

export default App;
```

혹은 name을 JSX문법을 활용해서 해결 하면 된다고 한다... 하지만 이방법은 통하지 않았다.. 별게의 문제였던 것 같다. 우선 나의 에러 코드는 다음과 같다.

```js
//원인 코드
    return (
        <div>
<LikeCard>
<h1>{userinfo.nickname} 님의 찜목록페이지 입니다!</h1>
</LikeCard>
```

처음에 if(userinfo){ 위에 코드 리턴} 식으로 작성 하였지만 해결 되지 않았다.. 또한 검색을 통한 방법도 사용했지만 역시나였다... 그래서 혹시나 하는 마음에 저번 맵함수 에러때를 떠올리면서 아래와 같이 작성하였다!

```js
//해결 코드
    return userinfo&&(
        <div>
<LikeCard>
<h1>{userinfo.nickname} 님의 찜목록페이지 입니다!</h1>
</LikeCard>
```

해결 되었다... 사실 왜 그런지는 모르겠다... 이것도 같은 원인일까 ? 한번 다시 파보도록 해야 될 것 같다.

<br />

## 4. 마무리..

이제 마이페이지 글쓴 목록 페이지만 하면 끝이다... 아직 데이터 베이스가 없어서... 진행하기가 어렵다... 심지어 내가 작성한 로직이 아니여서 조금 힘들다.. 동료에게 부탁해서 같이 하도록 해야 겠다..