## Class

---

Class문법은 constructior, prototype을 이용한 상속기능을 좀더 쉽게 표현해주는 문법입니다. 기존 옛날에 방식의 function을 활용한 방법과 별차이가 없습니다.

## Class 생성하기
클래스는 객체명 앞에 class 키워드를 이용해 생성할 수 있습니다.


```js
Class 부모(){
    constructor(){}
    method1(){}
    method2(){}
}
```

class 내부에는 크게 Construrctor와 method로 구성되어 있습니다!

<br />

## Constructor

Constructor는 class로 생성된 객체를 생성하고 초기화하기 위한 메서드입니다. 클래스 내부에 단 하나만 존재 할 수 있습니다.

```js
class 부모{
    constructor(이름,나이){
        this.name = 이름;
        this.age = 나이;
    }
}

```

Constructor 내부에는 변수 키워드가 아닌 this를 이용해서 변수를 생성합니다. 이때 this는 클래스가 생성할 인스턴스를 가르킵니다.

<br />

## Method

class 객체 내부에서 생성된 함수를 Method라고 부릅니다.

```js
class 부모{
    constructor(이름,나이){
        this.name = 이름;
        this.age = 나이;
    }
    sayHi(){
        console.log(`안녕 ${this.name}`)
    }
}
```

<br />

## Instanc

Instanc는 생성자 함수 같이 new 연산자와 함께 클레스 이름을 호출하면 해당 클래스의 인스턴스가 생성 됩니다!

```js
class 부모{
    constructor(이름,나이){
        this.name = 이름;
        this.age = 나이;
    }
    sayHi(){
        console.log(`안녕 ${this.name}`)
    }
}
//instanc
let 자식 = new 부모('lee',30);
자식.name // lee
자식.age  // 30
자식.sayHi  // 안녕 lee
```

<br />

## Extends

extends는 말그대로 확장키다! 연장시키다! 즉 다른 객체로 부터 상속 시킬수 있습니다. 기분적인 구조는 extends뒤에 상속 시킬 클래스를 적으면 됩니다.

```js
class A{}
class B extends A{}
```

<br />

## Super

super는 자식 클래스가 상위 클래스를 호풀 할 때 사용하는 메서드입니다.

```js
class 할아버지{
  constructor(name){
    this.성 = 'Kim';
    this.이름 = name;
  }
  sayHi(){
    console.log('안녕 나는 할아버지')
  }
}

class 아버지 extends 할아버지{
  constructor(name){
    super(name);
    this.나이 = 50;
  }
  sayHi2(){
    console.log('안녕 나는 아버지');
    super.sayHi();
  }
}

let 파덜 = new 아버지('만수');
파덜 // 아버지{성:"kim", 이름:"만수", 나이: 50}
파덜.sayHi2() // '안녕 나는 아버지' , '안녕 나는 할아버지'

```

super()는 상위 클래스에 값을 전달 시킬수 있고 super은 상위 클래스에서 프로퍼티나 값을 가져와서 사용할 수 있습니다.
