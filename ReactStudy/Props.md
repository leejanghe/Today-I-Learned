## Props

---

props는 컴포넌트의 속성을 의미하며 외부로부터 전달받은 값입니다. 또 한 상위 컴포넌트로 부터 전달 받을수 있고 props로 어떤 타입의 값도 넣어 전달 할 수 있도록 객체의 형태로 가집니다.

<br />

### Probs 어떻게 사용할까요 ?

---

1. 하위 컴포넌트에 전달하고자 하는 값과 속성을 정의<br />
2. props를 이용하여 정의된 값과 속성 전달<br />
3. 전달 받은 props를 렌더링<br />
<br />
props는 상위컴포넌트로 부터 받아 왔고 위에 있는 3가지 단계를 이해하면 Props의 개념은 정말 쉽습니다!  
<br />

### Probs 단계별예시 

---

아래 예시 코드를에서 `Joycoding은 Props 공부를 하고 있습니다!`라는 문장을 props를 활용해서 출력 해봅시다!  
프롭스는 상위에서 하위로 뿌려준다 라고 생각하기!

```js
import React from 'react'

function 상위컴포넌트(){
 const name = "Joycoding"
 const content = "Props 공부를 하고 있습니다!"

  return (
   
  <div>
    <하위컴포넌트 />
  </div>
  
    )
}

function 하위컴포넌트(){
  return <div></div>
}

export default 상위컴포넌트
```
<br />

1단계는 하위 컴포넌트에 전달하고자 하는 값과 속성을 정의를 해야 합니다. 아래와 같이 name과 content를 정의 하였습니다.<br />

```js
import React from 'react'

function 상위컴포넌트(){
 const name = "Joycoding"
 const content = "Props 공부를 하고 있습니다!"

  return (

  <div>
    <하위컴포넌트 name={name} content={content}/> // 1단계
  </div>
  
    )
}

function 하위컴포넌트(){
  return <div></div>
}

export default 상위컴포넌트
```
<br />

2단계는 props를 이용하여 정의된 값과 속성 전달 합니다 아래에 코드 참고!<br />
3단계는 전달 받은 props를 아래와 같이 렌더링 하면 `Joycoding은 Props 공부를 하고 있습니다!`가 출력됩니다.<br />

```js
import React from 'react'

function 상위컴포넌트(){ 
 const name = "Joycoding"
 const content = "Props 공부를 하고 있습니다!"

  return (
  <div>
    <하위컴포넌트 name={name} content={content}/> // 1단계
  </div>
  )
}

function 하위컴포넌트(props){ // 2단계
  return <div>{props.name + '은 ' + props.content}</div>  // 3단계
}

export default 상위컴포넌트
```