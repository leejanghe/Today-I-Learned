## 왜 이런 문제를 낸걸까? 나중에 이 문제에 대한 기본 개념이 있다면 정리하자!

---

### test1
재귀함수와 클로저 사용에 대한 이해

```js
function test1() {
  // TODO: 여기에 코드를 작성하세요.
  // 호출될때 함수를 리턴.. 그러면 리턴은 함수로 표현
  // 피보나치 수를 리턴 (피보나치 공식)fibonacci(n-1) + fibonacci(n-2);
  // 피보나치 기본 조건은 num < 2이하면 num 이 나와야됨

  let count = 0 //호출 횟수 카운터
  
  function fibonacci(num){
    if(num < 2){
      return num
     }
   return fibonacci(num-1) + fibonacci(num-2); 
 }
 //카운팅에 의해 호출
 return function(){
   count++
   return fibonacci(count-1)
 }
}
// 클로저를 활용한 메모제이션 기법
// 동일한 계산을 반복해야 할 때, 이전에 계산한 값을 메모리에 저장함으로써 
// 동일한 계산의 반복 수행을 제거하여 프로그램 실행 속도를 빠르게 하는 기술
```

---

### test2
재귀함수 활용 능력
```js
function test2(arr, id) {
  // TODO: 여기에 코드를 작성합니다.
  // childern 속성 가질 경우 arr과 같은구조
  // 재귀 함수로
  // id객체 없을경우 Null 리턴

  // 배열을 그냥 조회 할땐 (children 없을경우)
  // ex) input[1] // {id: 2, name: "ingi", children: Array(3)}
  // ex) input[1].id // 2
  let newArr= new Array();
  for(let el in arr) {
    if(arr[el].id === id) {
      return arr[el];
    }
    // 배열 요소에 children 속성 있을경우
    // childern속성이 배열이니까 ArrayisArray로 판별해서 재귀로 돌릴 배열에 넣기
    // ex) input[1].children[0] // {id: 3, name: "johnson"}
    else if(Array.isArray(arr[el].children)) {
      let childernArr = arr[el].children
      newArr = newArr.concat(childernArr);
    }
  }
    // childern안에 있는 배열도 재귀적으로 해결
  if(newArr.length >0) {
    return test2(newArr, id)
  }
  return null;
}
```

---

## test3
자료구조 인접행렬에 대한 이해

```js
function test3(insertEdges, removeEdges) {
  // TODO: 여기에 코드를 작성하세요.

    let max = 0;
    for (let el in insertEdges) {
        // max 변수를 0으로 할당하고, edges를 전부 순회해 제일 큰 숫자를 max에 할당합니다.
        //// edges의 한 요소에는 숫자 이외에 방향성도 있으니, 숫자까지만 slice를 하여 비교합니다.
        const curMax = Math.max(...insertEdges[el].slice(0, 2));
        curMax > max ? (max = curMax) : null;
    }
    // 인접 배열 만들
    const result = new Array(max + 1).fill(0).map((row) => new Array(max + 1).fill(0));
   
   // 두 정점간에 간선이 존재할 경우 1로
    insertEdges.forEach((edge) => {
        const [row, col] = edge;
            result[col][row] = 1;
            result[row][col] = 1;
  })
   //두 정점간에 간선이 존재하지 않을 경우 0으로
   removeEdges.forEach((edge) => {
        const [row, col] = edge;
            result[col][row] = 0;
            result[row][col] = 0;
  })

return result
}
```