# 문제 설명
수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.
마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.
<br />
 
# 제한사항
- 마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
- completion의 길이는 participant의 길이보다 1 작습니다.
- 참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
- 참가자 중에는 동명이인이 있을 수 있습니다.
<br />
 
# 입출력 예
participant	|completion|	return
:-:|:-:|:-:
[leo, kiki, eden]|	[eden, kiki]|	leo
[marina, josipa, nikola, vinko, filipa]|	[josipa, filipa, marina, nikola]	vinko
[mislav, stanko, mislav, ana]	|[stanko, ana, mislav]	|mislav
<br />
 
# 입출력 예 설명
예제 #1 <Br/>
leo는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.
예제 #2 <Br/>
vinko는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.
예제 #3 <Br/>
mislav는 참여자 명단에는 두 명이 있지만, 완주자 명단에는 한 명밖에 없기 때문에 한명은 완주하지 못했습니다.
<Br/>

# 문제 풀이
이문제를 풀기 위해서는 participant과 completion의 배열안에 있는 요소값을 비교해서 같이 않은 요소를 따로 출력하면 하면 된다! 그전에 두 배열을 요소를 쉽게 비교하기 위해 sort를 통해 내림차순을 한뒤 반복문이나 find메서드를 활용해서 요소 비교 후 같지 않은 요소를 출력하면 끝!


## Javascript

```js
function solution(participant, completion) {
    var answer = '';
 
    participant.sort();
    completion.sort();
 
    answer = participant.find((e, i) => e !== completion[i]);
 
    return answer;
 
}
```

```js
function solution(participant, completion) {
    var answer = '';
 
    participant.sort();
    completion.sort();
 
    for(let i=0; i<participant.length; i++){
        if(participant[i] !== completion[i]){
            answer = participant[i]
              return answer
        }
    }
}
```