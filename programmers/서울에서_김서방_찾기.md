# 문제 설명
String형 배열 seoul의 element중 Kim의 위치 x를 찾아, 김서방은 x에 있다는 String을 반환하는 함수, solution을 완성하세요. seoul에 Kim은 오직 한 번만 나타나며 잘못된 값이 입력되는 경우는 없습니다.
<br />

# 제한 사항
seoul은 길이 1 이상, 1000 이하인 배열입니다. <br />
seoul의 원소는 길이 1 이상, 20 이하인 문자열입니다. <br />
Kim은 반드시 seoul 안에 포함되어 있습니다. <br />
<br />

# 입출력 예
|    seoul    |      return       |
| :---------: | :---------------: |
| [Jane, Kim] | 김서방은 1에 있다 |
<br />

# 문제 풀이
반복문을 활용해서 서울이라는 배열안에 "Kim"이 있는지 없는지 조건을 써서 풀면 됩니다. 만약 
indexOf메서드를 알면 쉽게 풀수 있는 문제입니다.


## Javascript

```js
function solution(seoul) {
  for(let el in seoul){
      if(seoul[el]==="Kim"){
          return `김서방은 ${el}에 있다`
      }
  }
}
```

```js
function solution(seoul) {
  return `김서방은 ${seoul.indexOf("Kim")}에 있다`;
}
```