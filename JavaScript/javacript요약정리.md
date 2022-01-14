# 자바스크립트 요약 정리

## 데이터 타입

-  number  
-  정수(Integer) // 1,2,3,4  
-  소수(Float) // 1.55, 2.3423...  

number타입은 서로 연산기호를 이용하여 계산 가능

- String - 처음부터 끝까지 문자로 구성되어 있음 string은 "" or ''로 감싸서 표현

<br />

## 변수

변수는 어떤 데이터를 담아주는 저장 공간 변수를 지정할 땐 let, const, var가 있다. 대부분 const를 사용(항상 변하지 않은 값을 의미)

- let, const , var 정리

|변수키워드|선언|할당|
|:------:|:------:|:------:|
|let|재선언 금지|재할당 가능|
|const|재선언 금지|재할당 금지|
|var|재선언 가능|재할당 가능|


<br />

## booleans

booleans은 true, false 값으로 두개로 나눠 진다. 
- 추가적으로 null은 값이 없음 (컴퓨터에 값이 없을을 의도적으로 알리기 위해 채워진 값)
- undefined는 값이 정의되지 않음을 뜻한다. (변수에 값을 지정하지 않으면 메모리 상에 자리는 존재하지만 값이 채워지지 않음)

<br />

## array

배열은 데이터 자료형으로 []안에 데이터 자료를 넣을 수 있다.

```js
const arr = [1,2,3,4,5]

// 배열 조회는 [index]
arr[0]  // 1
arr[3]  // 4

// 배열 추가 (그외 unshift, shift 등 있음)
arr.push(6) // [1,2,3,4,5,6]
```


<br />

## object

object는 property를 가진 데이터를 저장하며, {}를 사용한다.

```js
// 객체는 키와 벨류로 구성되어 있으며 {}안에 있으면 객체 이다.
const obj = {
    name : 'joy',
    color : 'blue',
    age : 30,
    food: true,
}

// 벨류값 불러오기
// . or [] 로 벨류값을 불러올수 있다.
obj['name'] // joy
obj.age // 30

// 값 바꾸기
obj.name = 'coco';
console.log(obj.name) // coco

```

<br />
