## export default / import 문법

어떤 데이터 자료를 다른 js파일에서 사용하고 싶은 경우 export와 import 문법을 사용합니다. 예를 들어 data.js에 있는 변수를 app.vue에서 쓰고 싶을 경우 아래와 같습니다.

```js
// data.js
const teemo = ['버섯','화살촉']
export default teemoDate


// App.vue
import 작명 from './data.js파일경로'

```

만약 export 할게 많으면 구조분해 할당을 사용해서 받아올수 있습니다.

```js
// data.js
const teemo = ['버섯','화살촉']
const joycoding = ['지옥','아케인']
export {teemo, joycoding}


// App.vue
import 작명 from './data.js파일경로'
```

<br />

## 가져온 데이터 자료 저장

아래와 같이 자료를 저장하고 아래 movie를 활용해서 데이터 바인딩을 하면 됩니다.

```js
// data.js
//... 생략
export default movieDate


// App.vue
<div>
  <h4>{{movie[0].title}}</h4>
</div>



import data from './data.js파일경로'

data(){
    return {
        movie : data
    }
}
```

