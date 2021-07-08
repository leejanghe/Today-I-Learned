# 문제 설명

문자열 s는 한 개 이상의 단어로 구성되어 있습니다. 각 단어는 하나 이상의 공백문자로 구분되어 있습니다. 각 단어의 짝수번째 알파벳은 대문자로, 홀수번째 알파벳은 소문자로 바꾼 문자열을 리턴하는 함수, solution을 완성하세요.

<br />

# 제한 사항

문자열 전체의 짝/홀수 인덱스가 아니라, 단어(공백을 기준)별로 짝/홀수 인덱스를 판단해야합니다.  
첫 번째 글자는 0번째 인덱스로 보아 짝수번째 알파벳으로 처리해야 합니다.  

<br />

# 입출력 예

|     s     |  return   |
| :-------: | :-------: |
| "try hello world" | "TrY HeLlO WoRlD" |

<br />

# 입출력 예 설명

"try hello world"는 세 단어 "try", "hello", "world"로 구성되어 있습니다. 각 단어의 짝수번째 문자를 대문자로, 홀수번째 문자를 소문자로 바꾸면 "TrY", "HeLlO", "WoRlD"입니다. 따라서 "TrY HeLlO WoRlD" 를 리턴합니다.

<br />

# 문제 풀이
필터와 맵을써서 해결하려 했지만 너무 복잡해져서 알아보기 쉽게 로직을 작성했습니다. 문자열을 순회해서 띄어쓰기가 나올경우 인덱스는 0으로 할당하고 아니면 인덱스가 증가하면서 짝수일일때 소문자로 변환하고 아니면 대문자로 변할수 있도록 하였습니다.

```js
function solution(s) {
    let answer = '';
    let ind = 0;
    let slength = s.length
    
    for(let i = 0; i < slength; i++){
        if(s[i]===' '){
            answer = answer + ' '
            ind = 0
        }else{
            answer += ind % 2? s[i].toLowerCase():s[i].toUpperCase()
            ind++
        }
    }
    return answer;
}
```