## vue 이벤트 헨들러

자바스크립트에서는 어떤 이벤트 헨들러 함수를 쓸때 <div onclick=""> 식으로 자바스크립트를 넣습니다. 하지만 뷰에서는 @click="" 이걸 넣으면 됩니다. 

```js
//...생략

 <div v-for="(a,i) in products" :key="i">
    <h4>{{products[i]}}</h4>
    <p >{{ price[i] }} 만원</p>
    <button @click="like[i]++">좋아요!</button> <span>좋아여 :{{like[i]}}</span>
  </div>

//...생략
// 데이터 보관함
 data(){
    return {
      like : [0,0,0],
      products : ['강아지','고양이','악어'],
      price :['50','40','70']
    }
  },
```

@click 말고도 @mouseover, @input 등 다양한 이벤트 함수들이 존재합니다.

<br />

## 함수를 만들어서 사용 가능

뷰에서는 함수를 만들어서 데이터 바인딩이 가능합니다.

```js
//...생략

 <div>
    <h4>{{products[0]}}</h4>
    <p >{{ price[0] }} 만원</p>
    <button @click="increase">좋아요!</button> <span>좋아여 :{{like}}</span>
  </div>

export default {
  data(){
    return {
      like : 0,
      products : ['강아지','고양이','악어'],
      price :['50','40','70']
    }
  },
  methods:{
    increase(){
      this.like +=1;
    }
  },
}
```

밑에 methods:{}라는 항목을 만들어서 함수를 만들면 됩니다. 만들때 함수이름(){} 하면 끝입니다. 주의 할점은 위에 데이터를 가져도 쓰고 싶으면 꼭 this를 붙여서 사용해야 에러가 안납니다. 객체지향 문법과 동일합니다. 함수를 만들고 html로 가서 태그에 넣으면 끝입니다. () 써도 되고 안써도 상관 없습니다.