# 문제 설명

함수 solution은 정수 x와 자연수 n을 입력 받아, x부터 시작해 x씩 증가하는 숫자를 n개 지니는 리스트를 리턴해야 합니다. 다음 제한 조건을 보고, 조건을 만족하는 함수, solution을 완성해주세요.

<br />

# 제한 조건

x는 -10000000 이상, 10000000 이하인 정수입니다. <br />
n은 1000 이하인 자연수입니다.

<br />

# 입출력 예

|  x  |  n  |    answer    |
| :-: | :-: | :----------: |
|  2  |  5  | [2,4,6,8,10] |
|  4  |  3  |   [4,8,12]   |
| -4  |  2  |   [-4, -8]   |

<br />

# 문제풀이

i는 1부터 시작하여 n보다 작거나 같을때 까지 반복 순회하고  
i값이 순회하면서 각각 x값을 곱해서 배열안에 넣어주기!  

반복문에 대한 개념을 알고 있으면 충분히 풀수 있음


# 코드작성

## javascript

```js

function solution(x, n) {
    let answer = [];

    for(let i=1; i<=n; i++){
        answer.push(x*i)
    }
    return answer;
}
```

