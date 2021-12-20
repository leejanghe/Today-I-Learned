# TS 기본문법 정리

---

## 변수 타입 지정

```ts
let firstname :string = "lee"
firstname = 123  // 타입이 변경되면 에러가 납니다.
```

변수를 만들 때 타입지정이 가능합니다. 변수명 : 타입명 이렇게 씁니다.  
타입으로 쓸 수 있는 것들은 string, number, boolean, bigint, null undefined,[],{}이 있습니다.

<br />

## 배열 객체 타입지정

```ts
let catname :string[] = ['baba','koko']
let age :{age:number} = {age:5} // 문자열 '5' 넣으면 에러
```

<br />

## | 기호 사용 or 연산자 표현

```ts
let joycoding :string|number = '1123' //숫자 문자 둘다 가능
```

여러가지 타입의 데이터를 넣고 싶으면 | 기호를 이용하여 or연산자로 표현이 가능합니다. 위에 있는 예제는 숫자 혹은 문자열을 넣을수 있습니다.

<br />

## tpye키워드

```ts
type nameType = string | number;
let coco:nameType = 3123
```

타입키워드를 활용해 변수처럼 담아서 사용 가능합니다.

<br />

## literal type

```ts
type firstnameType = "lee" | 'kim'
let myname :firstnameType = "lee"
```

sting, number 타입뿐만 아니라 나만의 타입을 만들어 사용이 가능합니다. 저렇게 원하는 글자나 숫자를 입력하면 변수 앞으로 lee, kim 만 들어올 수 있습니다. 이를 literal type이라고 합니다.

<br />

## return cheack

```ts
function add(x:number) :number{ //인자가 넘버여야함
    return x+2
}
```

함수는 파라미터와 return 값이 어떤 타입일지 지정가능합니다. 실수로 다른 타입이 파라미터로 들어오거나 return될 경우 에러를 내줍니다. 함수는 return 타입으로 void를 설정가능한데 return이 없는지 체크할 수 있는 타입입니다.

<br />

## 함수 가능 불가능 예시

```ts
// 불가능
function addNum(x:number|string){
    return x+3
}

// 가능 
function minusNum(x:number|string){
    if(typeof x === 'number'){
        return x-3
    }
}
```

타입스크립트는 지금 변수의 타입이 확실하지 않으면 마음대로 연산할 수 없습니다. 항상 타입이 무엇인지 미리 체크하는 narrowing 또는 assertion 문법을 사용해야 허락해 줍니다.

<br />

## tuple type

```ts
type member = [number, boolean]
let koko:member = [50,true]
```

array 자료 안에 순서를 포함해서 어떤 자료가 들어올지 정확히 지정하고 싶으면 tuple 타입을 쓰면 됩니다. 대괄호[] 안에 들어올 자료의 타입을 차례로 적어주면 됩니다.

<br />

## 특정 속성 ?기입하기

```ts
type myobject = {
    name? :string,
    age : number
}

let baba :myobject ={
    name : 'lee',
    age : 30
}
```

객체 타입도 정의가 너무 길면 타입 키워드로 변수에 담아 사용 가능합니다. 타입 키워드 대신 비교적 최근에 나온 interface키워드를 이용해도 무방합니다. 차이점을 별로 없습니다. 특정 속성이 선택사항이면 물음표를 기입합니다.

<br />

## index signature

```ts
type myobject = {
    [key :string] :number,
}

let baba :myobject ={
    weight : 89,
    age : 30
}
```

객체안에 어떤 속성이 들어갈지 아직 모른다면 그냥 다 넣어서 타입지정이 가능합니다 이를 index signature이라고 합니다.

<br />

## class 타입설정

```ts
class Person{
    name;
    constructor(name :string){
        this.name = name;
    }
}
```

class도 타입설정이 가능합니다. 다만 중괄호 내에 미리 name 이렇게 변수를 만들어 놔야 컨스트럭터 안에서 this.name 사용이 가능합니다.