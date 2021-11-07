# Final_Project_dev #.19 (11.7)

---

## 1. 여태 내가 한 일들 

- 전반적인 css작업 완료
- 메인 리스트 페이지 완료

<br />

## 2. 내일 내가 할 일

- 터치 페이지 css작업 보완
- 메인 홈 페이지 css 작업 보완
- 마이페이지 찜목록 그리드 구도

<br />

## 3. 유용한 내용

오늘은 css에서 유용한 것 들에 대해 정리 해보고자 한다.

### 3-1. 배경화면 그라디 에니메이션 주기

백그라운드에서 그라디언트 에니메이션 효과를 줄 수 있다. 여기서 포인트는 gradient라는 변수를 keyframes를 활용해서 효과를 주는 것이다! 앞으로 유용하게 많이 쓸 것 같다! 

```css
.main-list-background{
  background: linear-gradient(-45deg, #2c3e50, #3498db, #f1f2b5, #135058);
  background-size: 400% 400%;
  animation: gradient 10s ease infinite;
  min-height: 100vh;
}

@keyframes gradient {
  0% {
      background-position: 0% 50%;
  }
  50% {
      background-position: 100% 50%;
  }
  100% {
      background-position: 0% 50%;
  }
}
```

<br />

### 3-2. 배경화면 새로고침 할 때 마다 다른 배경 화면 나오게 하기

정말 획기적인 사이트가 있다 자세한 사항은 아래 링크!

```css
.search_background{
    background-image: url('https://source.unsplash.com/category/nature/1190x3600');
    display: block;
    background-repeat: no-repeat;
    background-size : cover;
    max-width: 100%;
    height:25rem;
    background-position: center;
    /* margin: auto; */
    justify-content: center;
}
```

백그라운드 이미지에서 url만 넣으면 자동적으로 랜던 이미지들이 1190x3600사이즈로 출력된다.!  

[upsplash 주소](https://unsplash.com/developers)  
[생활코딩](https://opentutorials.org/module/2398/13868)

<br />

## 4. 마무리..

이제 일주일 남았다...별로 한것도 없는데 벌써 시간이 이렇게 녹아버리다니... 아무래도 백신 접종이 나한테 엄청난 영향을 끼친 것같다.. ㅠㅠ 너무 시간을 날린 것 같다.. 앞으로 남은 일주일 동안 마무리 작업과 동시에 슬슬 깃에다 합치는 작업을 진행해야 겠다!