## JSX란?

---

JSX는 자바스크립트의 확장 문법이며 XML과 매우 비슷하게 생겼습니다. JSX로 작성한 코드는 실행되기 전 코드가 번들링되는 과정에서 바벨을 사용하여 일반 자바스크립트 형태의 코드로 변환됩니다.

```javascript
function App() {
  return (
    <div>
      Hello
      <b>react</b>
    </div>
  );
}
```
이렇게 JSX로 작성된 코드를 일반 JS로 작성해보면

```javascript
function App() {
  return React.createElement("div", null, "Hello", React.createElement("b", null, "react"));
}
```

이런식으로 복잡하게 작성하게 됩니다. 이를 편하게 작성하기 위해 JSX를 사용합니다.

<br/ >

## JSX의 장점

---

### 1. 보기 쉽고 익숙하다

위에 JS로 작성한것과 JSX를 비교 해 보면 누가 봐도 JSX가 쉽고 가독성이 좋다는걸 알 수 있습니다. HTML와 매우 비슷해서 익숙하기까지 합니다.

### 2. 높은 활용도

JSX에서는 div나 span 같은 HTML 태그를 사용할 수 있을 뿐만 아니라 컴포넌트를 HTML 태그 쓰듯이 JSX 안에서 작성할 수 있습니다.

<br/ >

## JSX 문법

---

JSX는 편리한 문법이지만, 몇 가지 규칙을 준수해야 합니다.

### class 대신 className

JSX문법에서는 class가아닌 className을 사용해야 합니다.

```javascript
function App() {
	return <h1 className="title">hello!!!</h1>
}
```

### JSX 표현

JSX는 DOM 요소들을 렌더링 하는 기능 외에 JSX 안에서 자바스크립트 표현식을 사용 할 수 있습니다. 사용 방법은 JSX 내부에 { }로 감싸면 됩니다.

```javascript
function App() {
    const name = "joycoding"
	return <h1>hello {name}!!!</h1>
}
```
이렇게 하면 `hello joycoding`이 출력 됩니다.


### 태크로 감싸주기

JSX는 다수의 태그들을 리턴 할 수 없기 때문에 아래에 형제 노드가 있는 경우에는 묶어 줘야 됩니다. 만약에 의미가 없는 경우에는 빈 태그를 이용하면 됩니다. 

```javascript
function App() {
    const name = "joycoding"
	return (
        <>
        <h1>hello {name}!!!</h1>
        <h1>잘부탁합니다!</h1>
        </>
    );
}
```

### AND 연산자( && )를 사용한 조건부 렌더링

JSX에서는 AND연산자를 사용한 조건부 렌더링이 가능합니다. 또 한 코드 블럭 내에 삼항 연산자를 통해 표현 또한 가능합니다. (조건문 불가능)

```javascript
function App() {
    const name = "joycoding"
	return (
        <>
        <h1>hello!</h1>
        {name === "joycoding"? <h1>hello {name}!!!</h1> : <h1>아닙니다..</h1>}
        </>
    );
}
```

```javascript
function App() {
    const name = "joycoding"
	return (
        <>
        <h1>hello!</h1>
        {name &&  <h1>hello {name}!!!</h1>}
        {['😒','😭','😩'].map(el => (
            <h1>{el}</h1>
        ))}
        </>
    );
}
```