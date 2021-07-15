# 반복문 정리

---

## for문

for문은 초기값, 조건문, 증감문 구조를 가진 기본적인 반복문 입니다.

```js
//for문
let arr = [5,2,1,3]

for(let i =0; i < arr.length; i++){
    console.log(arr[i])
}
// 5,2,1,3
```

## forEach문

foreach구문의 인자로 callback함수를 등록할수 있고, 배열의 각 요소들이 반복될 떄 이 callback 함수가 호출됩니다. callback 함수에서 배열요소의 인덱스와 값에 접근할수 있습니다

```js
// #1 forEach문
let arr1 = ['가','나','다','라']
arr1.forEach((el)=>console.log(el))
// 가, 나, 다, 라

// #2 forEach문 
copy = []
arr = [4,2,1,3]
arr.forEach((el)=>copy.push(el))
// 4, 2, 1, 3
```

## for in

for in은 통상 오브잭트 자료형에 저장된 자료들을 하나씩 꺼낼때 사용합니다. 또한 열거형 속성이라면 어떤 자료든 추출이 가능합니다. 열거형 속성이랑 키와 키값으로 이뤄진 자료형을 말합니다. 배열도 인덱스와 요소값으로 이뤄진 열거형 속성입니다! 그래서 배열도 for in을 사용할수 있습니다. 다만 열거형이 확실한 오브잭트에 통상적으로 for in을 활용합니다.

```js
// for in
let obj = {name:'joycoding', age:30, hobby:'coding'}

for(let key in obj){
    console.log(obj[key])
}
// "joycoding", 30, "coding"
// 추가적으로 obj.hasOwnProperty(key)를 활용해서
// 오브잭트의 키값이 있는지 없는지 확인 해주는 함수가 있습니다.
```

## for of

for of는 for in 반복문과 매우 유사합니다. 다만 iterable인 자료형만 적용가능한 반복문입니다. 배열이나 문자열 처럼 index의 연속성이 있는 경우 for of를 사용합니다.

```js
// #1. for of 배열
let arr = [4,3,2,1]

for(let el of arr){
    console.log(el)
}
// 4, 3, 2, 1

// #2. for of 문자열
let str = 'hello'

for(let el of str){
    console.log(el)
}
// h, e, l, l, o
```

## for in과 for of 차이점

for in 반복문 : 객체의 모든 열거 가능한 속성(property)에 대한 반복  
for of 반복문 : [Symbol.iterator] 속성을 가지는 컬렉션 전용  

```js
//for in,of 차이
let obj = {
    a:1,
    b:2,
    c:3
}

for(let key in obj){
    console.log(key)
}
//a, b, c

for(let key of obj){
    console.log(key)
}
//Uncaught TypeError: obj is not iterable
```