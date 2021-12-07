## style 속성 데이터 바인딩

어떤 데이터를 변수로 만들고 `${}` 처럼 `백틱`기호를 쓰면 글자 중간에 변수 넣어 데이터 바인딩이 가능합니다.

```html
<template>
  <div class="post">
    <div class="post-header">
      <div class="profile" :style="{ backgroundImage : `url(${data.userImage})`}"></div> <!-- 프로필사진 -->
      <span class="profile-name">{{data.name}}</span>
    </div>
    <div class="post-body" :style="{ backgroundImage : `url(${data.postImage})`}"></div> <!-- 포스팅사진 -->
    <div class="post-content">
      <p>{{data.likes}} Likes</p>
      <p><strong>{{data.name}}</strong> {{data.content}}</p>
      <p class="date">{{data.date}}</p>
    </div>
  </div> 
</template>
```