## 최대 공약수와 최소 공배수(GCD/LCM)

(유클리드 호제법: Euclidean algorithm)  
두 수 a ,b(a > b)가 존재하고 최대 공약수를 구하는 함수가 GCD(a,b)이고 최소 공배수를 구하는 함수가LCN(a,b)일 때

### 최대공약수(GCD)
a % b === 0이면 a, b의 최대공약수는 b가 된다.  
a % b !== 0이면 GCD(b, a % b) 함수를 반복하여 실행하고 b % (a % b) === 0이 되는 순간 a % b가 최대공약수가 된다.  

### 최소공배수(LCM)
a, b의 곱에 a, b의 최대공약수로 나누어 나온 값이 a, b 두 수의 최소공배수가 된다.  
LCM(a, b) = (a * b) / GCD(a, b)  


이 두가지 조건을 참고하여 아래와 같이 코드로 작성하였습니다.

```js
//최대 공약수와 최소 공배수(GCD/LCM) 코드

function solution(n, m) {
    //최대 공약수
  const gcd = function(n, m){
      if(n%m===0){
          return m
      }else{
          return gcd(m, n%m)
      }
  }
    //최소 공배수
  const lcm = function(n, m){
      return (m*n) / gcd(n,m)
  }
    //배열안에 최대 공약수와 최대 공배수 넣어서 리턴하기 
  return [gcd(n, m), lcm(n, m)];
}
```
