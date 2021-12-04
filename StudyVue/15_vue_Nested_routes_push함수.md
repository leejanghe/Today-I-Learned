## vue Nested routes & push 함수

특정 페이지 안에서 route를 나누고 싶을 때 사용한다. 예를들어 /detail/0/comment로 접속하고 싶다면 /detail/0 뒤에 children을 만들어 추가해주면 된다. 여기서 주의할 것은 children의 path에 /을 제외해서 상대경로로 적어준다.

```html
<!-- Comment 컴포넌트 -->
<div>
    <h4>안녕하세요</h4>
</div>
```

예를 들어 위에 있는 children 컴포넌트를 만들었다고 가정을 하고 시작했을때 이컴포넌트를 아래와 같이 등록 해준다.

```js
// router
import { createWebHistory, createRouter } from "vue-router";
import List from './views/List.vue';
import Home from './views/Home.vue';
import Detail from './views/Detail.vue';

//아까 만든 컴포넌트 import
import Comment from './views/Comment.vue';

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
    // 핵심 (Nested routes)
    children: [
      {
        path: "comment",
        component: Comment,
      }
    ]
  },
  {
    path: "/:anything(.*)",
    component: Home,
  },
];

const router = createRouter({
  history: createWebHistory(),
  routes,
});

export default router; 
```

그리고 nested routes에 해당하는 것을 보여주고 싶을 때 <router-view>를 사용한다.

```html
<template>
  <div>
    <h4>상세페이지</h4>
    <h5>{{blog[$route.params.id].title}}</h5>
    <p>{{blog[$route.params.id].content}}</p>
    <router-view></router-view>
  </div>
</template>
```

그럼 /detail/0/comment로 접속하면 Detail.vue + Comment.vue가 보이는 것이다.

<br />

## $router.push 함수

$route는 현재라미터경로, $router는 페이지 이동관련 기능이다.

```html
<div v-for="(a,i) in blog" :key="i">
      <h5 @click="$router.push('/detail/'+i)">{{blog[i].title}}</h5>
      <p>{{blog[i].date}}</p>
  </div>
```
페이지 이동시켜주는 함수 $router.push()를 사용할수 있습니다. 

```html
  <div>
    <h4>상세페이지</h4>
    <h5>{{blog[$route.params.id].title}}</h5>
    <p>{{blog[$route.params.id].content}}</p>
    <router-view></router-view>
    <h5 @click="$router.go(-1)">뒤로가기</h5>
  </div>
```

$router.go()을 사용하면 페이지를 앞, 뒤로 움직일 수 있다. 뒤로가기는 $router.go(-1)로 구현하면 된다.