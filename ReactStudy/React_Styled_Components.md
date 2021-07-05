## Styled Componets란 ?

---

스타일 컴포넌트는 css나 sass와 같이 class, id, tag name을 가져와서 쓰지 않고, 별도의 스타일 컴포넌트를 생성하여 태그에 쓰는 것을 말합니다. 스타일 컴포넌트는 **ui단위를 나누어 컴포넌트화 하기 때문에 재사용이 가능**하며 props로 속성 까지 전달하여 조건을 붙일 수 있어 여러모로 다양한 이점이 있습니다.
<br />


## Styled Componets의 특징!

---

1. 화면에 어떤 컴포넌트가 렌더링 되었는지 추적해서 해당하는 컴포넌트에 대한 스타일을 자동으로 삽입합니다.</br>
2. 스타일컴포넌트는 스스로 **유니크한 `clssName`을 생성**해서 중복이나 오타로 인한 버그를 줄여줍니다.</br>
3. 스타일 컴포넌트는 모든 스타일 속성이 특정 컴포넌트와 연결되어 있어 **추가 및 삭제가 매우 편리**합니다.</br>
4. `className`을 일일이 수동으로 관리할 필요 없이 **React의 props나 전역속성 기반**으로 컴포넌트에 속성을 부여하기 떄문에 간단하고 직관적입니다.</br>
5. 다른 css파일들을 검색하지 않아도 되기 때문에 코드의 크기가 커지더라도 **유지보수가 어렵지 않습니다**</br>
6. 개별 컴포넌트마다 기존의 css를 이용해서 스타일 속성을 정의하면 됩니다. 그**이외 것들은 스타일 컴포넌트가 알아서 처리합니다**</br>
<br >


## Styled Componets 시작하기!

---

설치는 매우 간단합니다. 터미널창에 아래와 같이 스타일 컴포넌트를 설치해주고 해당 컴포넌트 페이지에서 `import styled from 'styled-components'`해서 불러오면 됩니다.
<br />

```js
npm install--save styled-components
//or
npm add styled-components
```
<br />

## Styled Componets 만들기

---

스타일 컴포넌트는 변수를 선언하여 컴포넌트를 지정하고 styled 불러와서 ``안에 스타일을 지정해서 사용하면 됩니다
<br />

```js
const 컴포넌트이름 = styled.태그명`스타일을 지정하세염`
```
<br >

## Styled Componets 활용해보기

---

스타일컴포넌트를 만든 것을 활용해 봅시다!!!
<br />

```js
import styled from "styled-components"; //스타일 컴포넌트 불러오기

// Title컴포넌트 h1태그 스타일링
const Title = styled.h1`
  font-size: 35px;
  color: pink;
`;

// Contents컴포넌트 p태그 스타일링
const Contents = styled.p`
  font-size: 20px;
`;

//변수를 담아 컴포넌트 안에 넣을수도 있어염!!!
const message = "안녕하세요!! 스타일 컴포넌트 공부 정말 재미있습니다!";

// 감싸주는 태크입니다!!!
const Wrapper = styled.div`
  padding: 5em;
  background: green;
  text-align: center;
  color: yellow;
`;

export default function App() {
  return (
    <Wrapper>
      <Title>Hello joycoding!</Title>
      <Contents>{message}</Contents>
    </Wrapper>
  );
}

```
<br />
결과는 코드펜에서 복사해서 확인해보시길!!!
<br >

## Styled Componets 중첩 스타일링

---

스타일 컴포넌트는 중첩 스타일링을 위해 SCSS 와 같은 전처리 기능을 자동으로 지원합니다. 중첩 스타일링을 하기 위해서는 `appersand(&)` 기호를 사용하면 됩니다.
<br />

```js
import styled from "styled-components"; //스타일 컴포넌트 불러오기

// Title컴포넌트 h1태그 스타일링
// 만약 타이틀컴포넌트에 호버 효과를 주고싶으면 & 기호 사용해서 중첩하기!
const Title = styled.h1`
  font-size: 35px;
  color: pink;
  &:hover{
      background : green;
  }
`;

//...생략

```
<br />

## Styled Componets props 활용하기

---

스타일 컴포넌트는 내부에서 삼항연산자를 활용해서 스타일링이 가능합니다.
<br />

```js
import styled from "styled-components"; //스타일 컴포넌트 불러오기

// Button컴포넌트 button태그 스타일링
// 표현할때는 ${(프롭스)=>(삼항연산자)}
const Button = styled.button`
   background: ${(props) => (props.point ? "blue" : "white")};
   color: ${(props) => (props.point ? "white" : "blue")};
`;

export default function App() {
  return (
    <div>
      <Button>hello<Button> 
      <Button point>joycoding<Button>
    </div>
  );
}
```
<br />
첫번째 hello 버튼은 프롭스가 없기 때문에 하얀색 바탕에 파란 글이 나오고 두번째 joycoding버튼은 파란색 바탕에 흰글씨가 출력 됩니다.
<br />

<br />

## Styled Componets 재사용 하기

---

스타일 컴포넌트의 큰 장점은 이미 만들어진 컴포넌트를 받아와서 재사용 할 수 있습니다. 방법은 간단합니다. 변수를 지정하고 `styled(재사용하고싶은 컴포넌트)`로 지정해주면 됩니다.

```js
import styled from "styled-components"; //스타일 컴포넌트 불러오기

// Button컴포넌트 button태그 스타일링
// 표현할때는 ${(프롭스)=>(삼항연산자)}
const Button = styled.button`
   background: ${(props) => (props.point ? "blue" : "white")};
   color: ${(props) => (props.point ? "white" : "blue")};
`;

// 만약에 hello버튼의 속성을 가져와서 border값을 추가 한 버튼을 만들고 싶다면 ?
const borderBtn = styled(Button)`
   border: 2px solid green;
   border-radius: 3px;
`
//borterBtn 컴포넌트를 추가합니다.
export default function App() {
  return (
    <div>
      <Button>hello<Button> 
      <Button point>joycoding<Button>
      <borderBtn>coco!!</borderBtn>
    </div>
  );
}
```
<br />

borderbtn버튼은 hello버튼의 기본속성과 더블어 볼더속성이 추가된 상태를 볼수 있습니다.
<br />

