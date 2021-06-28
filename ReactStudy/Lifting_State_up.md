## State 상태 끌어 올리기

---

상태 끌어 올리기를 알기전 리엑트에서 데이터가 어떻게 흘러가는지를 파악해야 합니다. 리엑트에서 컴포넌트는 단일 책임 원칙으로 하나의 컴포넌트는 한가지 일만 합니다. 또한 컴포넌트는 바깥에서 props를 이용해 데이터 속성을 전달 받을수 있습니다. 즉 데이터를 전달하는 주체인 부모 컴포넌트에서 자식 컴포넌트로 하샹식 데이터 흐름을 갖습니다. 이것이 기본적인 리엑트의 데이터 흐름입니다. 하지만 개발을 하다보면 자식 컴포넌트가 부모 컴포넌트에 영향을 줄 때가 있습니다. 이러한 역뱡항 흐름을 해결하는 방법이 `상태끌어올리기`입니다. 상태를 변경시키는 함수를 하위 컴포넌트로 probs로 전달하여 해결 할 수 있습니다.

### 데이터 흐름 정리
1. 리엑트는 단일 책임 원칙과 단방향 흐름입니다.</br>
2. 컴포넌트 바깥에서 props를 활용해서 데이터 속성을 전달 받습니다.</br>
3. 리엑트의 데이터 흐름은 상위컴포넌트에서 하위 컴포넌트로 하샹식 흐름입니다.</br>

### 상태 끌어 올리기 정리
1. 만약 하위컴포넌트가 상위 컴포넌트에 영향을 준다면 이것은 상태 끌어 올리기 입니다.</br>
2. 상태 끌어 올리기는 리엑트의 역방향 흐름을 해결하는 방법입니다.</br>
3. 상태를 변경시키는 함수를 하위 컴포넌트로 프롭스로 전달하여 해결합니다.</br>
</br>

## 예시를 통해 State 상태 끌어 올리기 이해하기

---

```js
import React, { useState } from "react";
import "./styles.css";

const currentUser = "김코딩";

function Twittler() {
  const [tweets, setTweets] = useState([
    {
      uuid: 1,
      writer: "김코딩",
      date: "2020-10-10",
      content: "안녕 리액트"
    },
    {
      uuid: 2,
      writer: "박해커",
      date: "2020-10-12",
      content: "좋아 코드스테이츠!"
    }
  ]);

  const addNewTweet = (newTweet) => {
    setTweets([...tweets, newTweet]);
  }; // 이 상태 변경 함수가 NewTweetForm에 의해 실행되어야 합니다.

  return (
    <div>
      <div>작성자: {currentUser}</div>
      <NewTweetForm />
      <ul id="tweets">
        {tweets.map((t) => (
          <SingleTweet key={t.uuid} writer={t.writer} date={t.date}>
            {t.content}
          </SingleTweet>
        ))}
      </ul>
    </div>
  );
}

function NewTweetForm({ onButtonClick }) {
  const [newTweetContent, setNewTweetContent] = useState("");

  const onTextChange = (e) => {
    setNewTweetContent(e.target.value);
  };

  const onClickSubmit = () => {
    let newTweet = {
      uuid: Math.floor(Math.random() * 10000),
      writer: currentUser,
      date: new Date().toISOString().substring(0, 10),
      content: newTweetContent
    };
    // TDOO: 여기서 newTweet이 addNewTweet에 전달되어야 합니다.
  };

  return (
    <div id="writing-area">
      <textarea id="new-tweet-content" onChange={onTextChange}></textarea>
      <button id="submit-new-tweet" onClick={onClickSubmit}>
        새 글 쓰기
      </button>
    </div>
  );
}

function SingleTweet({ writer, date, children }) {
  return (
    <li className="tweet">
      <div className="writer">{writer}</div>
      <div className="date">{date}</div>
      <div>{children}</div>
    </li>
  );
}

export default Twittler;
```
</br>

### step1. 최상위 컴포넌트 찾기
리엑트에서 데이터 흐름은 부모에서 자식으로 하향식 흐름입니다. 그래서 상태 끌어 올리기를 하기 위해서는 최상위 컴포넌트를 찾아 줍시다!!!(아래 step 확인하기)
</br>

### step2. 상위 컴포넌트 내에 변경 함수 찾기
하위컴포넌트가 상위 컴포넌트에 영향을 주는 변경 함수를 찾아야 합니다. (아래 step 확인하기)
</br>

### step3. 하위 컴포넌트에 프롭스를 활용해 변경함수 전달
전달해줄 변경함수에 프롭스를 정의하고 하위컴포넌트에 프롭스를 받아 줍니다 (아래 step 확인하기)
</br>

### step4. 변경 함수 활용해서 상태 끌어 올리기!
상위 컴포넌트에서 변경함수를 전달 받았으면 활용을 해야겠죠 ? (아래 step 확인하기)
</br>

```js

function Twittler() {  //step1 상위 컴포넌 트찾기
  const [tweets, setTweets] = useState([
  ... 생략

  const addNewTweet = (newTweet) => { //step2단계 변경 함수 찾기
    setTweets([...tweets, newTweet]);
  }; // 이 상태 변경 함수가 NewTweetForm에 의해 실행되어야 합니다.

  return (
    <div>
      <div>작성자: {currentUser}</div>
      <NewTweetForm onButtonClick={addNewTweet}/>  //step3 프롭스를 활용해서 변경함수 전달하기
      <ul id="tweets">
        {tweets.map((t) => (
          <SingleTweet key={t.uuid} writer={t.writer} date={t.date}>
            {t.content}
          </SingleTweet>
        ))}
      </ul>
    </div>
  );
}

function NewTweetForm({ onButtonClick }) { //step3 프롭스를 활용해서 변경함수 전달하기
  const [newTweetContent, setNewTweetContent] = useState("");

  const onTextChange = (e) => {
    setNewTweetContent(e.target.value);
  };

  const onClickSubmit = () => {
    let newTweet = {
      uuid: Math.floor(Math.random() * 10000),
      writer: currentUser,
      date: new Date().toISOString().substring(0, 10),
      content: newTweetContent
    };
    // TDOO: 여기서 newTweet이 addNewTweet에 전달되어야 합니다.
    onButtonClick(newTweet) // step4 변경함수 활용해서 상태 끌어 올리기
  };

 ... 생략

export default Twittler;
```

## 최종정리

하위컴포넌트가 상위 컴포넌트에게 영향을 주는 상황이면 상태 끌어 올리기를 통해 해결을 합니다. 상태 끌어 올리기는 상위 컴포넌트 안에 있는 변경함수를 프롭스를 활용해서 하위컴포넌트에 전달하는 방식을 말합니다!