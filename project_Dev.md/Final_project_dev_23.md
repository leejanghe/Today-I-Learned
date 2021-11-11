# Final_Project_dev #.23 (11.11)

---

## 1. 여태 내가 한 일들 

- 메인 페이지 (검색 기능 일부 수정)
- 메인 페이지 최종 마무리

<br />

## 2. 내일 내가 할 일

- 시연영상, 업스트리밍 머지작업, 데이터 베이스 (이미지, 음원 찾기)

<br />

## 3. 에러 헨들링

### 버튼 클릭시 reload되는 현상

문제 원인 - button이 form 태그 안에 있을 경우 발생한다. 일반 버튼일 경우 상관 없지만 form 태그 안에 버튼이 있는 경우에는 따로 type을 설정하지 않으면 reload현상이 나타납니다.

```js
//문제 코드
<form>
<button className="user_update_btn" onClick={updateUser}>수정</button>
</form>

// 해결 코드
<form>
<button type="button" className="user_update_btn" onClick={updateUser}>수정</button>
</form>
```

form 태그 안에서의 button 태그는 기본적으로 클릭시 submit 이벤트를 실행시키도록 되어있음을 알게 되었습니다.

<br />

[참고 레퍼런스1](https://dololak.tistory.com/763)  
[참고 레퍼런스2](https://devhoma.tistory.com/90)  
[참고 레퍼런스3](https://stackoverflow.com/questions/7803814/prevent-refresh-of-page-when-button-inside-form-clicked)  

<br />

## 4. 수정 사항

### 1. 검색 기능

수정 이유 - 검색 할때 검색 키워드에 대한 리스트들은 잘 나오나 전체 리스트에서 어떤 이미지를 클릭했을때 해당 이미지에 대한 리스트들이 다시 나오는 문제가 생겼다. 문제 코드는 아래와 같다.

```js
  const [moveImgs, setMoveImgs] = useState([])
  const [moveCurrentImgs, setMoveCurrentImgs] = useState({
      title:''
  })
    
    
    const search = ({ title }) => {
      if (moveCurrentImgs.title !== title) {
        
        console.log('title',title)
    
        setMoveCurrentImgs(
          {title})
      }
    }
    
    const filterByImg = (img) => {
        let isTrue = true;
        if (moveCurrentImgs.title) {
         isTrue = isTrue && img.title === moveCurrentImgs.title;
        }
        return isTrue;
      }
```

문제 원인은 상태관리를 잘못했다. 현재 이미지를 클릭하게 되면 그 클릭한 이미지와 똑같은 제목을 가진 이미지들이 다 출력 되는 것이다. 그래서 필터로 걸러 낼 수 있도록 따로 필터만 하는 상태 관리 할 수 있도록 아래와 같이 다시 수정해 보았다.

```js
  const [moveImgs, setMoveImgs] = useState([])
  const [moveCurrentImgs, setMoveCurrentImgs] = useState({})
    
  const [filterImg, setFilterByImg] = useState({
    title:""
  })
    

    const search = ({ title }) => {
      if (filterByImg.title !== title) {
        console.log('title',title)
        setFilterByImg(
          {title})
      }
    }

    const filterByImg = (img) => {
  
      let isTrue = true;
      if (filterImg.title) {
       isTrue = isTrue && img.title === filterImg.title;
      }
      return isTrue;
    }
```

이렇게 했더니 내가 원하는 대로 수정되었다. 한편으로는 처음 사용했던 코드를 활용해서 카테고리 버튼으로 활용 할 수 있을 거라는 생각이 들었다. 나중에 써먹어야 될 것 같다.

<br />

### 검색기능2

수정 이유 - 생각해보니 검색 할 때 데이터 정보에 없는 제목을 검색했을때 빈리스트만 나오는 것보다 검색한 데이터가 없다라는 장치가 필요 할 것 같았다... 처음 코드는 아래와 같다.

```js
//...생략
{
moveImgs && moveImgs.map((moveimg, idx) => <MovelistCard
handleMoveCardClick={handleMoveCardClick}
moveimg={moveimg} 
key={idx.id}/>)
}
```

처음에 검색한 데이터가 없을 경우 어떻게 데이터가 없음을 알려 줄 수 있을지 고민을 많이 했다... 근데 생각보다 간단했다. 

```js
...생략
{
moveImgs.length > 0? moveImgs.map((moveimg, idx) => (<MovelistCard
handleMoveCardClick={handleMoveCardClick}
moveimg={moveimg} 
key={idx.id}/>)):<MainNotFound/>
}
```

해답은 데이터의 길이였다. 뿌려준 데이터이미지 길이가 0보다 커야 이미지들이 출력되고 아니면 MainNotFound 컴포넌트를 뿌려주면 되는 것이였다. 왜 마무리 시점에서 이런 해결 방법들이 떠오르는 것일까 ? ㅋㅋ 신기하다

<br />

## 4. 마무리..

뭔가 끝이 보이니 많이 아쉽다... 사람이 참 이상한게 꼭 시간이 촉박할때 머리가 트이면서 안보이는 문제를 해결하게 되고 있으면 괜찮을 것 같은 아이디어나 기능이 떠오르게 된다... 어쨋든 더이상 욕심은 금지다.. 일단 마무리 작업을 해야 그 이후에 시연 영상이나, 개인발표, 피피티 등 아직 할 것들이 많이 남아 있기 때문이다.. 여튼 이번 프로젝트 통해서 많이 배우고 얻어가는 느낌이다. 프로젝트 끝나고도 사이드 프로젝트를 통해 실력을 많이 키워야 겠다!