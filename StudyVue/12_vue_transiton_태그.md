## vue 애니메이션 태그

vue에선 애니메이션을 주는 특별한 태그가 있습니다. 일반 적인 css로 할땐 아래와 같습니다.

```html
<div class="start" :class="{end : isModal}">
<Modal @closeModal="isModal = false" :clickModal="clickModal" :isModal="isModal"/>
</div>
```

핵심 포인트는 :class={클래스명 : 조건} 입니다. 이럴때 isModal이 true일 때 class명인 end가 적용이 됩니다.

```css
.start {
  opacity: 0;
  transition: all 1s;
}

.end {
  opacity: 1;
}
```

그렇다면 vue에서 제공하는 transition 태그를 이용하기 위해선 그냥 감싸고 name="클래스명" 으로 작성하면 됩니다. 예시는 아래와 같습니다.

```html
<transition name="fade">
<Modal @closeModal="isModal = false" :clickModal="clickModal" :isModal="isModal"/>
</transition>
```

css는 아래와 같고 퇴장시 애니메이션을 주고 싶으면 스타일에서 enter 대신 leave로 바꾸면 됩니다.

```css
/* 시작시 */

/* 애니메이션 동작 전 상태 */
.fade-enter-from {
  opacity: 0;
  transform: translateY(-1000px);
}

/* 애니메이션 동작 중 상태 */
.fade-enter-active {
  transition: all 1s;
}

/* 애니메이션 동작 후 상태 */
.fade-enter-to {
  opacity: 1;
  transform: translateY(0px);
}

/* 퇴장시 */

/* 애니메이션 동작 전 상태 */
.fade-leave-from {
  opacity: 1;
}

/* 애니메이션 동작 중 상태 */
.fade-leave-active {
  transition: all 1s;
}

/* 애니메이션 동작 후 상태 */
.fade-leave-to {
  opacity: 0;
}
```