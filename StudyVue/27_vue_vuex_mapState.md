## vuex mapstate

state를 vue파일에서 꺼내 쓸 때 $store.state.변경할거 이런식으로 꺼내 썼는데 이게 너무 길고 줄이고 싶으면 mapState라는 함수를 사용할 수 있습니다. 그전에 computed라는 항목을 알고 넘어가야 합니다.

<br />

## computed

함수를 만들때 methods:{}안에 만들수 있는데 실은 computed:{}안에도 만들수 있습니다. 다만 차이점은 methods는 함수를 부를때마다 안의 코드가 실행되고 computed는 함수를 불러도 실행이 안됩니다. 즉 일종의 계산결과 저장공간이라고 생각하면 됩니다. 트위터 기입 날짜, 인스타 그램 기입 날을 입력할 떄 좋습니다.

<br />

## mapState 사용법

사용할때 무조건 import를 해서 사용할수 있습니다. 그리고 꺼내야할 상태가 100개가 있다고 가정했을 때 mapState를 쓰면 알아서 computed에다가 state를 등록해 줍니다.

```js
//사용법 1
import {mapState} from 'vuex'

computed : {
    ...mapState(['state1','state2'])
}
```

그리고 객체 자료형을 넣으면 이름 변경도 가능합니다.


```js
//사용법 2
import {mapState} from 'vuex'

computed : {
    ...mapState({작명,'state이름1'})
}
```

또 한 mutations 함수도 쉽게 가져다 쓸 수 있습니다. 그래서 $store.commit('함수1') 가아닌 함수1()로 쓸수있어서 코드를 줄일수 있는 장점이 있습니다!

```js
//사용법 3
import {mapState} from 'vuex'

computed : {
    ...mapState({작명,'state이름1'})
    ...mapMutations(['함수1','함수2'])
}
```