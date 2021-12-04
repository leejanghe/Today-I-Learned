## vue url 파라미터

URL 파라미터를 만들기 위해 router의 path안에 "/detail/:id"과 같이 /:작명을 하면 된다. (그럼 /detail/0, 1, 2... 가능) 예를들어 해당 라우터의 순번을 표현하려면 {{blog[해당하는 id번호].title}} 에서 []안에 $route.params.id를 넣는다.현재 URL 정보는 $route에 담겨있기 떄문에 $route.params는 파라미터자리에 기입된 것을 알려준다.

```js
// router
import { createWebHistory, createRouter } from "vue-router";
import List from './views/List.vue';
import Home from './views/Home.vue';
import Detail from './views/Detail.vue';

const routes = [
  {
    path: "/",
    component: Home,
  },
  {
    path: "/list",
    component: List,
  },
  {
    path: "/detail/:id",
    component: Detail,
  },
];

const router = createRouter({
  history: createWebHistory(),
  routes,
});

export default router; 
```

위와 같이 라우터 설정을 하고 아래와 같이 url파라미터를 활용할수 있습니다.

```html
<!-- Detail 컴포넌트 -->
<div>
    <h4>상세페이지</h4>
    <h5>{{blog[$route.params.id].title}}</h5>
    <p>{{blog[$route.params.id].content}}</p>
    <router-view></router-view>
    <h5 @click="$router.go(-1)">뒤로가기</h5>
  </div>
```

정리하자면 $route.params.id는 router의 path안에 :파라미터 작명한 것을 넣어주면 URL의 파라미터를 가져옵니다. (꼭 id가 아닌 작명이 가능)