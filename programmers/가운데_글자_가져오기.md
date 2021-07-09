# 문제 설명

단어 s의 가운데 글자를 반환하는 함수, solution을 만들어 보세요. 단어의 길이가 짝수라면 가운데 두글자를 반환하면 됩니다.


<br />

# 제한사항

s는 길이가 1 이상, 100이하인 스트링입니다.


<br />

# 입출력 예

|    s    | return |
| :-----: | :----: |
| 'abcde' |  'c'   |
| 'qwer'  |  'we'  |


<br />

# 문제 풀이

## Javascript

조금만 생각하면 쉽게 풀수 있는 문제입니다. 짝수일때는 가운데 글자가 2개가 출력되고 홀수일때는 한개가 출력된다라는 사실을 알수 있습니다. 그래서 substr을 활용해서 문자열의 길이에서 2를 나눴을때 0이나오면 1개가 출력되도록 하고 아니면 2개가 출력할수 있도록 설정하였습니다. 여기서(2.5는 2를 의미합니다)
<br />

```js
function solution(s) {
    let 문자길이 = s.length;
    let 짝수 = s.substr(문자길이/2 -1,2)
    let 홀수 = s.substr(문자길이/2,1)
    
    return 문자길이%2==0 ? 짝수 : 홀수;
}
```

다르게 풀기

```js
function solution(s) {
  var answer = "";
  var sum = parseInt(s.length / 2);
  if (s.length % 2) return s[sum];
  else return s[sum - 1] + s[sum];
  return answer;
}
```