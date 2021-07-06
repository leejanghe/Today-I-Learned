## 고차함수 인자 활용하기

---

리엑트 할때 수많은 데이터를 화면에 출력할때 고차함수 map을 활용하면 엄청 편리합니다! 근데 하면서 인자를 두개씩 받아 와서 하는 경우가 있습니다. 예를 들어 `arr.map((ele, index)=>)` 식으로 왜 ele, index 두개인자가 왜 들어오는거지 ? 하면서 혼란을 겪을 때가 있습니다. 사실 알고보면 엄청 기본적인 내용이고 아차 할수 있습니다!
<br />

## 콘솔로그를 활용해서 이해해보기!

---

콘솔로그를 활용하면 직관적으로 ele와 index가 무엇인지 직관적으로 파악할수 있습니다.
<br />

```js
const menuArr = [
    { name: 'Tab1', content: 'Tab menu ONE' },
    { name: 'Tab2', content: 'Tab menu TWO' },
    { name: 'Tab3', content: 'Tab menu THREE' },
  ];

  //위와 같은 데이터를 활용해봅시다

  menuArr.filter((ele,index)=>console.log(ele)) //무엇이 출력 될까요 ? 아래와 같이 출력됩니다.
    // { name: 'Tab1', content: 'Tab menu ONE' }
    // { name: 'Tab2', content: 'Tab menu TWO' }
    // { name: 'Tab3', content: 'Tab menu THREE' }

  menuArr.filter((ele,index)=>console.log(index)) //무엇이 출력 될까요 ?
  // 0 1 2  가 출력 됩니다. 
```
<br />
그러면 여기서 ele.name을 하면 뭐가 나올까요 ? Tab1,Tab2,Tab3이 출력됩니다! 즉 ele는 요소값이 출력이 되고 index는 해당 배열의 index값이 출력 된다라는 사실을 알수 있습니다.
<br />

## filter를 활용해서 삭제해보기!

---

우리는 위에 있는 예제를 통해서 두개의 인자가 어떤식으로 활용되는지 알아봤습니다!! 그래서 위에 있는 예제를 바탕으로 3번째 데이터를 삭제해보겠습니다!
<br />

```js
const menuArr = [
    { name: 'Tab1', content: 'Tab menu ONE' },
    { name: 'Tab2', content: 'Tab menu TWO' },
    { name: 'Tab3', content: 'Tab menu THREE' },
  ];

let removeTab3 = menuArr.filter((ele,index)=> index !== 2)
remveTab3 // 콘솔창에 확인해보기! 서번째 데이터가 삭제 된것을 확인할수 있습니다!

let removeTab3 = menuArr.filter((index)=> index !== 2)//그렇다면 이렇게하면 어떤 결과가 ??
remveTab3 // 어떤 결과가 나오는지 확인해보기!
```
<br />
아무런 영향이 없습니다. filter에서 3개의 인자를 받을수 있습니다. filter(요소, 인덱스, 배열)이기때문에 인자를 하나를 받아오면 요소값이 순회가 되기때문에 아무런 변화가 없습니다!!! 맵도 같은 맥락이니 참고하시길!!!
