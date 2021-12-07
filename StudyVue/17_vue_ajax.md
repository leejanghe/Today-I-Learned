## ajax 요청

Ajax는 빠르게 동작하는 동적인 웹 페이지를 만들기 위한 개발 기법의 하나입니다. Ajax는 웹 페이지 전체를 다시 로딩하지 않고도, 웹 페이지의 일부분만을 갱신할 수 있습니다.

<br />

## ajax 설치

axios 라이브러리를 쓰든가 기본 fetch 함수를 쓰면 된다. fetch API는 브라우저 비교적 최신 기능이지만 호환성 문제때문에 axios를 이용한다. <script>에서 axios를 import 해온 뒤, axios.get(), axios.post()식으로 사용하면 된다.

```
npm i axios
```

<br />

## ajax를 활용한 더보기 기능

만약 'https://데이터있는사이트'에 /more0.json, /more1.json... 식으로 데이터가 있다고 가정하고 우선 <script>에서 methods에 more()이라는 함수를 등록한 뒤 더보기 버튼에 @click="more"로 함수를 넣어준다.

```html
  <button @click="more">더보기</button>
```

그리고 data()에서 moreThen을 기본값을 0으로 준 뒤 클릭할 때마다 1씩 추가되어 axios.get으로 more0, more1를 불러와서 push 추가시킨다.

```js
 data(){
    return {
      inStar : data,
      moreThen : 0,
    }
  },
  components: {
    Container,
  },
  methods :{
    more(){
      axios.get(`https://codingapple1.github.io/vue/more${this.moreThen}.json`)
      .then((result)=>{
        console.log(result.data);
        this.inStar.push(result.data);
        this.moreThen++;
      })
    }
  }
```

더보기 버튼을 누르면 axios로 json파일을 get해와서 .then 성공한다면 result의 data를 inSrar 데이터안에 push해서 추가해주면 데이터가 추가되어 화면에 출력된다.