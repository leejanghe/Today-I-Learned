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


## JSX의 장점

---

### 1. 보기 쉽고 익숙하다

위에 JS로 작성한것과 JSX를 비교 해 보면 누가 봐도 JSX가 쉽고 가독성이 좋다는걸 알 수 있습니다. HTML와 매우 비슷해서 익숙하기까지 합니다.

### 2. 높은 활용도

JSX에서는 div나 span 같은 HTML 태그를 사용할 수 있을 뿐만 아니라 컴포넌트를 HTML 태그 쓰듯이 JSX 안에서 작성할 수 있습니다.  



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
</br>

### JSX 표현

JSX는 DOM 요소들을 렌더링 하는 기능 외에 JSX 안에서 자바스크립트 표현식을 사용 할 수 있습니다. 사용 방법은 JSX 내부에 { }로 감싸면 됩니다.

```javascript
function App() {
    const name = "joycoding"
	return <h1>hello {name}!!!</h1>
}
```
이렇게 하면 `hello joycoding`이 출력 됩니다.

</br>

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
</br>

### 삼항연산자와 AND 연산자( && )를 사용한 조건부 렌더링

JSX에서는 AND연산자를 사용한 조건부 렌더링이 가능합니다. 또 한 코드 블럭 내에 삼항 연산자를 통해 표현 또한 가능합니다. (if 조건문 불가능)

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
</br>

### undefined를 렌더링하지 않기
리액트 컴포넌트에서는 undefined를 렌더링하는 상황을 만들면 오류가 발생하게 됩니다.
값이 undefined일 수도 있다면, OR( || ) 연산자를 이용하여 오류를 방지할 수 있습니다.
```javascript
function() {
	const name = undefined;
	return { name || <h1>undefined가 맞습니다.</h1> }
}
```
OR 연산자는 전자가 true면 전자를 반환하고 false면 후자를 반환시킵니다.
위의 코드는 undefined가 false로 인식되기 때문에 후자가 반환됩니다.

</br>

### 인라인 스타일링
리액트에서 스타일을 적용할 때는 객체 형태로 작성해야 합니다. 주의 할 점은 font-size 같은 - 문자가 포함되어 있는 속성은 -를 떼고 카멜 표기법으로 표기해줘야 합니다. ex) fontSize, backgroundColor
```javascript
function() {
	const name = '리액트';
	const style = {
      width: '100px',
      height: '100px',
      fontSize: '16p',
      backgroundColor: 'blue'
    }
	return <div style={style}> {name} </div>
}
```
이런 식으로 인라인 스타일링을 줄 수 있습니다.