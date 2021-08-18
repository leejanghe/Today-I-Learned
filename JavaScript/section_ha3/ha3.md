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