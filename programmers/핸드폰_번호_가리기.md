# 문제 설명

프로그래머스 모바일은 개인정보 보호를 위해 고지서를 보낼 때 고객들의 전화번호의 일부를 가립니다.
전화번호가 문자열 phone_number로 주어졌을 때, 전화번호의 뒷 4자리를 제외한 나머지 숫자를 전부 \*으로 가린 문자열을 리턴하는 함수, solution을 완성해주세요.

<br />

# 제한 조건

s는 길이 4 이상, 20이하인 문자열입니다.

<br />

# 입출력 예

| phone_number  |      return      |
| :-----------: | :--------------: |
| '01033334444' | '**\*\*\***4444' |
|  '027778888'  |   '**\***8888'   |

<br />

# 문제풀이

이문제를 풀기 위해서는 repeat메서드와 substring메서드를 알면 쉽게 접근 할 수 있는 문제입니다.repeat은 반복하는 함수입니다.<br />
"반복할거".repeat(반복할수) 라고 생각하면 됩니다.<br />
그래서 "".repeat(phone_number.length - 4);  여기 줄은 ""가 폰넘버의 길이의 -4만큼 반복한다라고 생각하면 됩니다.<br />

substing메서드와 length속성을 사용해 특정 문자열의 마지막 문자를 추출 할 수 있습니다. <br />
그래서 phone_number.substring(phone_number.length - 4);로 작성 하였고 <br />
이렇게 작성한 로직을 두개의 변수로 분리하여 두변수를 더해서 반환 하였습니다! <br />
코드를 직관적으로 줄여 보니 아래 처럼 표현도 가능합니다!


# 코드작성

## javascript

```js
// #1 변수나눠서 풀기(substring)
function solution(phone_number) {
    const star = "*".repeat(phone_number.length - 4);
    const lastNum = phone_number.substring(phone_number.length - 4);
    return star+lastNum;
}
```

```js
// #2 한번에 리턴때리기(substr)
function solution(phone_number) {
    return "*".repeat(phone_number.length-4) + phone_number.substr(-4,4);
}
```