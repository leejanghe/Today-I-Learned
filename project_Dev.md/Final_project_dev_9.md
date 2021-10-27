# Final_Project_dev #.9 (10.27)

---

## 1. 오늘 내가 한 일들 

- 메인 페이지 : 이미지 리스트 페이지 구도 잡기(다시)
- 메이 페이지 : 카드클릭시 터치 페이지로 기능 구현
- 메인 페이지 : 음악과 이미지 같이 데이터 받기
- 메인 페이지 일부 구도 수정

<br />

## 2. 내일 내가 할 일

- 이미지 리스트에서 이미지 클릭시 전송 성공 모달창 구현
- 카트리스트에 버튼 달기
- 터치페이지 그리드 구상

<br />

## 3. 알게 된점

React Router로 렌더링하는 컴포넌트에 prop 전달할때 데이터가 전달되지 않은 문제점을 발견하였다. 코드는 아래와 같다

```js
    // 문제 코드
        <Route path='/MainPage/ImgList' exact component={ImgList} 
        img={imgs} 
        handleCardClick={handleCardClick}/>

        <Route path='/MainPage/Touch' exact component={Touch} 
        img={currentImgs}/>
```

위와같이 페이지 이동은 잘 되었으나 프롭스로 전달한 데이터는 전달되지 않았다...위에 방법은 프롭스 전달을 무시해버리게 된다고 한다. 그래서 참고 자료를 바탕으로 아래와 같이 수정해 보았다.

```js
    // 해결 코드
         <Route path='/MainPage/ImgList'
        render={()=> <ImgList imgs={imgs} 
        handleCardClick={handleCardClick}/>}/>

        <Route path='/MainPage/Touch' 
        render={()=> <Touch img={currentImgs}/>}/>
```

Route 컴포넌트의 component prop을 사용하지 말고 render prop을 사용하는 것이다. render prop은 함수형 컴포넌트를 수용하고, 위의 방법을 사용했을 때 불필요하게 다시 마운트 되지 않을 뿐만 아니라 프롭스 전달도 잘된다.


<br />

## 4. 참고 레퍼런스

[라우터 프롭스 전달](https://sustainable-dev.tistory.com/117)  
[오디오 넣는 방법](https://mjmjmj98.tistory.com/123)  
[오디오 태그](http://tcpschool.com/html-tags/audio)  

<br />

## 5. 마무리...

3일만에 대충 어느정도 구도가 잡히고 있어서 뿌듯하다... 하지만 디테일적으로 보면 수정할게 한두가지가 아니다... 일단 큰틀을 만들고 좁혀서 진행해야 될 것 같다... 작은거부터 하려고 하니 시간이 오래걸리기 떄문이다... 어쨋든 3일 동안 많은 시행 착오를 겪었는데 많이 배운 느낌이다... 이런 시간이 좀 더 길었으면 좋겠다! 생각보다 재미있다! 에러와의 고통도 있었지만 그걸 해결하는 짜릿함이 너무 좋다! 내일은 백신 접종으로 인해 많이 할 수 있을지 의문이다...ㅠㅠ