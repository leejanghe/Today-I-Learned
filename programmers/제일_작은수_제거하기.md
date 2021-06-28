# 문제 설명

정수를 저장한 배열, arr 에서 가장 작은 수를 제거한 배열을 리턴하는 함수, solution을 완성해주세요. 단, 리턴하려는 배열이 빈 배열인 경우엔 배열에 -1을 채워 리턴하세요. 예를들어 arr이 [4,3,2,1]인 경우는 [4,3,2]를 리턴 하고, [10]면 [-1]을 리턴 합니다.

<br />

# 제한 조건

arr은 길이 1 이상인 배열입니다. <br />
인덱스 i, j에 대해 i ≠ j이면 arr[i] ≠ arr[j] 입니다.

<br />

# 입출력 예

|    arr    | return  |
| :-------: | :-----: |
| [4,3,2,1] | [4,3,2] |
|   [10]    |  [-1]   |

<br />

# 문제 풀이

처음엔 솔트 정렬을 활용해서 제일 작은 수를 끝에다 배치하고 슬라이스를 활용해서 제일 작은 값 빼고 나머지가 출력 될수 있도록 로직을 작성하였습니다.. 테스트 케이스는 통과하였지만 제출이 안되고 오류가 발생했습니다 ㅠㅠ


## javascript

```js
// 테스트 케이스는 통과 제출은 오류
function solution(arr) {
    if(arr.length <= 1){
        return [-1]
    }
    
    let restArr = arr.sort((a,b)=>b-a)
 
 
    return restArr.slice(0,-1)
 
}
```
그래서 아래에 코드 처럼 정석으로 풀었더니 통과가 되었습니다!

```js
function solution(arr) {
    if(arr.length <= 1){
        return [-1]
    }
    let arrMin = Math.min(...arr)
    let result = []
    for(let i in arr){
        if(arrMin !== arr[i]){
            result.push(arr[i])
        }
    }
    return result
}
```
어쨋든 이문제의 핵심은 스프레드 문법을 사용해서 배열안에 있는 최소값을 구하고 반복문을 통해서 최소값과 일치하지 않는 값들을 배열에 담아서 반환하면 됩니다! 