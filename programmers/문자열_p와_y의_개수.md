문자열 s는 알파벳으로만 이루어져 있습니다.
# 입출력 예
|    s    | answer |
| :-----: | :----: |
| pPoooyY |  true  |
|   Pyy   | false  |
# 입출력 예 설명
입출력 예 #1
'p'의 개수 2개, 'y'의 개수 2개로 같으므로 true를 return 합니다.
입출력 예 #2
'p'의 개수 1개, 'y'의 개수 2개로 다르므로 false를 return 합니다.
<br />

# 문제 풀이
이문제의 핵심은 P와 Y의 개수를 비교하는 문제입니다. 그래서 해당 문자열을 전부 대문자로 만들어주고 스플릿을 통해 P와 Y를 쉽게 비교할수 있도록 하였습니다. 그런다음 filter메서드를 통해서 P와 Y만 출력 되도록 하였고 거기에 length를 붙여서 길이를 비교하여 블린값을 리턴하도록 하였습니다!


## Javascript

```js
function solution(s){
    let isUpper = s.toUpperCase().split('')
    let isP_length = isUpper.filter((el)=>el === "P").length
    let isY_length = isUpper.filter((el)=>el === "Y").length
    
    return isP_length === isY_length
}

```

```js
function solution(s) {
  var answer = true;
  let pCount = 0;
  let yCount = 0;
  for (let i = 0; i < s.length; i++) {
    if (s[i].toUpperCase() === "P") pCount++;
    if (s[i].toUpperCase() === "Y") yCount++;
    answer = pCount === yCount;
  }
  return answer;
}
```