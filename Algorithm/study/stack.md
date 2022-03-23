# stack

Last In First Out이라는 개념을 가진 선형 자료구조이다. 즉 나중에 들어온것이 먼저 나간다는 뜻이다.
바닥이 막힌 상자를 생각하면 편하다.

```js
const stack = [];

//Push
stack.push(1);
stack.push(2);
stack.push(3);
console.log(stack); // [1,2,3]

//Pop
stack.pop();
console.log(stack); // [1,2]

//Get top
console.log(stack[stack.length-1]) // 2
```

## 문제예제

`()`로 스택 실습 코드 만들기

```js
function solution(s){
    const stack = [];

    for(c of s){
        if(c === "("){
            stack.push("(")
        }else{
            if(stack.length === 0){
                return false;
            }
            stack.pop()
        }
    }
    return stack.length === 0;
}
```

또 다른 표현으로 가능

```js
function solution(s){
    let count = 0;

    for(c of s){
        if(c === "("){
            count += 1;
        }else{
            if(count === 0){
                return false;
            }
            count -= 1;
        }
    }
    return count === 0;
}
```