## 출제 의도를 파악하고 해당 문제의 개념 정리하기

### test1

최대공약수와 최소공배수 개념 정리하기

```js
function test1(A, B) {
// TODO: 여기에 코드를 작성하세요.
// 문제유형은 최대공약수와 최소공배소
// A와 B의 길이를 통해 최대공약수가 가정 큰 정사각형의 변
// 문제예시에서 A=20, B=8 일때 A는 2^2 * 5  B는 2^3 승이기때문에 2^2가 최대 길이를 가지는 수
  const gcd = function(A,B){
    if(A%B===0){
      return B
    }else{
      return gcd(B, A%B)
    }
  }
  return gcd(A,B)
}
```

<br />

### test2

순열에 대한 이해 순열 코드 참고하기

```js
function test2 (n, m) {
  // TODO: 여기에 코드를 작성하세요.
  let result = []
  let arrNum = []

// n의 숫자만 큼 배열로 뽑아내기
  for(let i=1; i<=n; i++){
    arrNum.push(i)
  }

// 탈출조건 및 버킷에 결과 담기
  let rcs = (arr, bucket=[], time) => {
    if(time===0){
      result.push(bucket)
      return;
    }
// 배열의 원소 하나씩 넣고 빼기 (슬라이스, 재귀)
    for(let i = 0; i < arr.length; i++){
      let arrSlice = arr.slice();
      arrSlice.splice(i,1);
      rcs(arrSlice, bucket.concat(arr[i]), time-1)
    }
  }
// 재귀사용해서 탈출할때까지 진행
  rcs(arrNum, [], m)
  return result.map((el)=>parseInt(el.join("")))
};
```

<br />

### test3


```js
function test3(board, operation) {
  // TODO: 여기에 코드를 작성하세요.
const ROW = board.length
const COL = board[0].length

  // lookup table
const DIR = {
    'U': [-1, 0],
    'D': [1, 0],
    'L': [0, -1],
    'R': [0, 1]
  }

  // isValid
const isInside = Array(ROW).fill(-1).map((el)=>Array(COL).fill(-1))


let result = 0;
let [dY,dX] = [0,0]

// 그냥 UDLR 각각으로 조건주기
  for (let i = 0; i < operation.length; i++) {
    if(operation[i]==="U"){
      if(dY-1>=0){
        dY -= 1
      } else {
        continue
      }
    } else if(operation[i]==="D"){
      if(dY+1<ROW){
        dY += 1
      }else {
        continue
      }
    } else if(operation[i]==="L"){
      if(dX-1>=0){
        dX -= 1
      }else {
        continue
      }
    } else if(operation[i]==="R"){
      if(dX+1<COL){
        dX += 1
      }else {
        continue
      }
    }

    if(isInside[dY][dX]===-1){
      result = result + board[dY][dX]
      isInside[dY][dX] = true;
    }
  }
  return result;
};
```