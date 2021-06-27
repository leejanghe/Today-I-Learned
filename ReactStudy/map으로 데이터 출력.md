## Map으로 데이터 출력하기

---

리엑트에서 데이터를 직접 코드에 작성하는 것을 하드코딩이라고 합니다. 이러한 하드코딩은 직관적이여서 좋지만 출력해야할 데이터가 수만가지라면 코드가 길어지고 작성해야할 작업이 많아집니다. 그래서 여러 데이터를 렌더링 할 때 map메서드를 사용하면 편하게 데이터를 출력할수 있습니다! 아래 예제는 하드코딩을 한 예시입니다.

```js
import React from 'react'

function Mapdata(){
  const datas = [
    {id:1, name:'joycoding', content: '리엑트짱'},
    {id:2, name:'띠모', content: '안녕하세염'},
    {id:3, name:'바바', content: '고양이기워영'},
    {id:4, name:'코코코', content: '리엑트 재밌당'},
    {id:5, name:'핫도구', content: '맵을 활용하자'},
    {id:6, name:'하드코딩', content: '이지이지이지'},
  ]

  return (
    <>
  <div>
    <h3>{datas[0].name}</h3>
    <p>{datas[0].content}</p>
  </div>
  <div>
    <h3>{datas[1].name}</h3>
    <p>{datas[1].content}</p>
  </div>
  <div>
    <h3>{datas[2].name}</h3>
    <p>{datas[2].content}</p>
  </div>
  <div>
    <h3>{datas[3].name}</h3>
    <p>{datas[3].content}</p>
  </div>
  <div>
    <h3>{datas[4].name}</h3>
    <p>{datas[4].content}</p>
  </div>
  </>
     )
}

export default Mapdata
```
<br />

## map으로 표현하기

---

이번엔 위의 하드코딩을 아래 코드와 같이 map으로 표현할수 있습니다. 변수를 지정해서 사용해도 상관없고 주의할 점은 key값을 꼭 넣어 줍시다!! 넣지 않아도 작동은 잘되나 key값을 넣어야 한다는 경고가 나옵니다.

```js
import React from 'react'

function Mapdata(){
  const datas = [
    {id:1, name:'joycoding', content: '리엑트짱'},
    {id:2, name:'띠모', content: '안녕하세염'},
    {id:3, name:'바바', content: '고양이기워영'},
    {id:4, name:'코코코', content: '리엑트 재밌당'},
    {id:5, name:'핫도구', content: '맵을 활용하자'},
    {id:6, name:'하드코딩', content: '이지이지이지'},
  ]

  // 변수를 활용해서 리턴 중괄호 안에다 mapdata 넣어도 됩니다.
  // const mapdata = datas.map((el)=>
  // <div key={el.id}>
  //   <h3>{el.name}</h3>
  //   <p>{el.content}</p>
  //   </div>
  // )

  return (
    <>
  <div key={el.id}>
    {
      datas.map((el)=>
      <div key={el.id}>
     <h3>{el.name}</h3>
     <p>{el.content}</p>
     </div>
      )
    }
  </div>
  </>
     )
}

export default Mapdata
```