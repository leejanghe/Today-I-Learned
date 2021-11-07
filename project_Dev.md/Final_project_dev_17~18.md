# Final_Project_dev #.12~16 (11.4~11.6)

---

## 1. 여태 내가 한 일들 

- 맨 위로가기 버튼 구현
- 메인페이지 전반적인 수정 작업
- 검색기능 구현
- 사이드바 수정 -> 헤더 메뉴로
- 케러셀 구현


<br />

## 2. 내일 내가 할 일

- 메인페이지 서버와 연결
- 데이터베이스에 필요한 이미지 및 음원 서치
- 전반적인 css 작업

<br />

## 3. 유용한 내용

### 3-1. 캐러셀

메인페이지 홈에서 웹 서비스에 대한 이해도를 위해 캐러셀을 활용해 보도록 하였다! 참고 레퍼런스를 찾는 도중 react-slick에서 캐러셀을 활용 할 수 있는 라이브러리를 알게 되었다. 사용법은 아래와 같다.

<br />

```
npm i react-slick --save
npm i slick-carousel
```

우선 위에 두개를 설치를 한다.

```js
import Slider from "react-slick";
import "slick-carousel/slick/slick.css";
import "slick-carousel/slick/slick-theme.css";
```

설치 후 사용 할 컴포넌트 안에서 위와 같이 import를 해준다.

```js
const settings ={
        autoplay: true,
        autoplaySpeed: 2000,
        infinit:true,
        dots:true,
        slidesToShow: 1,
        // arrows:true,
        slidesToScroll:1,
        // lazyLoad:true
    }

     return (
        <div>
            <Slider {...settings}>
            <div>
              1
            </div>
             <div>
              2
             </div>
            <div>
              3
             </div>
             <div>
              4
            </div>
            </Slider>
        </div>
    )
}

```

이런식으로 작성하면 된다. 매우 유용하다! 나중에도 활용해서 써먹어야 겠다!

<br />

### 3-2. 위로 가기 버튼

스크롤을 계속하다 보면 맨 위로 가고 싶을 때까 있는데 이때 위로 가기 버튼이 있으면 편리 할 것 같아서 구현해 보았다.

```js
  const [ScrollY, setScrollY] = useState(0);
    
    const handleFollow = () => {
      setScrollY(window.pageYOffset);
      if(ScrollY > 100) {
      } 
    }
  
    const handleTop = () => {  // 클릭하면 스크롤이 위로 올라가는 함수
      window.scrollTo({
        top: 0,
        behavior: "smooth"
      });
      setScrollY(0);  // ScrollY 의 값을 초기화
    }
  
    useEffect(() => {
      const watch = () => {
        window.addEventListener('scroll', handleFollow)
      }
      watch();
      return () => {
        window.removeEventListener('scroll', handleFollow)
      }
    })
```

위로가기 로직이고 여기서 버튼을 만들어서 onClick에 handleTop을 넣어주면 된다.

<br />

### 3-3. 검색기능 구현

처음에 상위 컴포넌트에서 이미지리스트들을 관리 하고 타이틀 기준으로 검색 할 수 있도록 상태 관리를 하엿다. 또 한 서치함수를 상태 끌어올리기를 통해 영향이 갈 수 있도록 프롭스로 전달 하였고 필터함수를 통해 검색이 될 수 있도록 구현하였다.

```js
function Heal({isLogin, userinfo, handleLogout}){


// 움직이는 이미지  
  const [moveImgs, setMoveImgs] = useState(DummyUpData)

    // console.log('img',moveImgs)

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

  //... 생략
   <Route path='/heal/moveimg' 
        render={()=><MoveImgList 
            search={search}
            moveCurrentImgs={moveCurrentImgs} 
            moveImgs={moveImgs.filter(filterByImg)}
            handleMoveCardClick={handleMoveCardClick}
            />}
        />
  //... 생략      
```

search 함수를 프롭스로 전달 받은 자식 컴포넌트에서 상태 끌어올리기를 통해 제목 검색을 할 수 있도록 구현하였다.

```js
import { useState } from 'react'
import '../maincomponent/maincss/Search.css'
import { Link } from 'react-router-dom'

function Search({search}) {
  const [text, setText] = useState('')

console.log('textdest',text)

  const handleChange = (e) => {
    setText(e.target.value)
    console.log(e.target.value)
  }

  const handleKeyPress = (e) => {
    if (e.type === 'keypress' && e.code === 'Enter') {
      handleSearchClick()
    }
  }

  const handleSearchClick = () => {
    search({ 
      title : text })
  }

  return (

 <div className="search_background">
     <div className="search_container">
         <div >
            <h1 className="search_text">주제를 검색해보세요!</h1>
         </div>
         <div className="search_input_center">
         <input id="search_input" type="text" value={text} onChange={handleChange} placeholder="&#61442;" onKeyPress={handleKeyPress} />
         {/* <button className="search_btn">Search</button> */}
         </div>
  <div>
  <Link to = "/heal/touch" ><button className="search_btn">Touch 바로가기</button></Link>
  </div>
     </div>
     
     {/* search_input_center */}
   
 </div>
  )
}

export default Search
```

<br />

## 4. 마무리..

너무 어렵다... 근데 재미있다... 이제 거의 마무리 단계여서 더이상 욕심은 사치이다... 아직 보완 할 부분이 너무 많은데... 다음 일정을 소화하기 위해선 하는데 까지 마무리를 해야 할 것 같다... 나중에 혼자서 사이드 프로젝트를 통해 이것 저것 만들어 보는 시간을 가져야 겠다!