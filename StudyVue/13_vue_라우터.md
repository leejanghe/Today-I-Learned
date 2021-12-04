## vue-router

우선 vue-router를 설치를 합시다. 보통 4버전이 범용적으로 씁니다.

```
npm i vue-router@4
```

주의할점은 npm run serve를 하기 전에 설치하는게 바람직합니다(모든 라이브러리)

<br />

## 라우터 파일 만들기

src폴더 안 아무데나 라우터 파일을 만듭니다. 라우터의 기본적인 양식은 아래와 같습니다.

```js
import { createWebHistory, createRouter } from "vue-router";


const routes = [
  {
    path: "/경로",
    component: import한 컴포넌트,
  },
];

const router = createRouter({
  history: createWebHistory(),
  routes,
});

export default router;
```

위와 같이 라우터를 추가적으로 사용 하고 싶을때 변수 routes 안에 객체를 추가해서 사용하면 됩니다.

<br />

## main.js 등록

main.js에서 아래와 같이 라우터 등록을 하면 됩니다.

```js
import { createApp } from 'vue'
import App from './App.vue'
import router from './router.js'

createApp(App).use(router).mount('#app')
```

<br />

## 라우터 사용

위와 같은 스텝을 진행 했다면 사용할 html에서 <router-view /> 태그를 추가하면 됩니다. 또 한 라우터 태그에 데이터 바인딩도 아래와 같이 할 수 있습니다.

```js
<router-view :data ="data"></router-view>
```

<br />

## 페이지 이동 링크

뷰도 리엑트 처럼 페이지 링크태그가 있습니다. 사용은 아래와 같습니다.

```js
<router-link to="/">Home</router-link>
```

위와 같이 라우터링크 태그에 to="경로" 를 하면 경로 설정이 완료 됩니다.