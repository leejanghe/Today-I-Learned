## Rest parameter

---

Rest parameter는 자바스크립트에서 추가된 ES6 신문법입니다. 함수를 만들때 ...을 사용해서 파라미터들을 담아줍니다. rest파라미터는 모든 파라미터를 중괄호로[]감싸준 파라미터라는 뜻입니다.

```js
function testRestPara(...rest){
    console.log(rest)
}
testRestPara(1,3,4,2,3,1)
// [1, 3, 4, 2, 3, 1]
```


### 다른예시

아래 예시는 1부터 3은 a,b,c로 쓰고 그 뒤에 나오는 모든 파라미터는 중괄호에 감싸서 배열이 됩니다.

```js
function testRestPara(a,b,c,...rest){
    console.log(rest)
}
testRestPara(1,2,3,4,5,6,7)
// [4,5,6,7]
```

rest parameter 문법은 다루기가 쉽고 간단해서 자주 사용하는 문법중 하나입니다! 위에 예제만 확실히 이해한다면 다양하게 응용할수 있습니다!

