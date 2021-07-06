# 문제 설명

임의의 양의 정수 n에 대해, n이 어떤 양의 정수 x의 제곱인지 아닌지 판단하려 합니다.
n이 양의 정수 x의 제곱이라면 x+1의 제곱을 리턴하고, n이 양의 정수 x의 제곱이 아니라면 -1을 리턴하는 함수를 완성하세요.

<br />

# 제한 사항

n은 1이상, 50000000000000 이하인 양의 정수입니다.

<br />

# 입출력 예

|  n  | return |
| :-: | :----: |
| 121 |  144   |
|  3  |   -1   |

<br />

# 입출력 예 설명

입출력 예#1 <br />
121은 양의 정수 11의 제곱이므로, (11+1)를 제곱한 144를 리턴합니다.

입출력 예#2 <br />
3은 양의 정수의 제곱이 아니므로, -1을 리턴합니다.

<br />

# 문제 풀이
이문제에 대한 수도코드를 작성하자면 <br />
  
1. n이 제곱근인지 확인하는 조건만들기  
2. n이 제곱근이면 n의 루트값 +1을 해서 제곱하기  
3. 아니면 -1을 리턴하기  
  
이렇게 3가지로 나눌수 있습니다. 그래서 아래와 같이 코드를 작성했습니다.


## javascript

```js
// 테스트 케이스는 통과 제출은 오류
function solution(n) {
    
    let 루트값 = Math.sqrt(n) // 11
    let 제곱근 = Math.floor(Math.pow(루트값,2))
   
    let isTrue = Math.sqrt(n) + 1
    let result = Math.floor(Math.pow(isTrue,2))
    
    return n === 제곱근 ? result : -1
}
```
<br />
테스트 케이스는 전부 통과했지만 채점케이스에서 3개가 통과가 안됬습니다... ㅠㅠ 그래서 정수인지 판별해주는 함수 Number.isInterger()를 사용해서 아래와 같이 최적화 하여 코드를 작성했습니다.
<br />

```js
function solution(n) {
    let num = Math.sqrt(n)
    return Number.isInteger(num) ? Math.pow(num+1,2) : -1;
}
```