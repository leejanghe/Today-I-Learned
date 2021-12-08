## 글 발행 버튼 만들기

v-if를 조건을 활용해서 만들면 된다. 데이터 step번호에 따라 보이게 만들수 있습니다. 

```html
<li v-if="step ===1" @click="step++">Next</li>
<li v-if="step ===2" @click="publish">발행</li>
```

게시물 발행기능에서 data에 내가 발행한 게시물을 추가하려면 게시물 data에 들어있는 객체에 똑같은 자료를 만든 다음 this.inStar에 추가하면 됩니다.

```js
data(){
    return {
      inStar : [...data],
      moreThen : 0,
      step : 0,
      upLoadUrl : '',
      myWrite : '',
    }
  },
```

아래와 같이 발행기능 함수를 만들어 주면 되고 unshift()를 활용해서 데이터를 추가하는 자바스크립트 문법을 사용하면 됩니다.

```js
methods :{
publish(){
      let myPost = {
      name: "Kim Hyun",
      userImage: "https://placeimg.com/100/100/arch",
      postImage: this.upLoadUrl,
      likes: 36,
      date: "May 15",
      liked: false,
      content: this.myWrite,
      filter: "perpetua"
      };
      this.inStar.unshift(myPost);
      this.step = 0;
    }
}
```