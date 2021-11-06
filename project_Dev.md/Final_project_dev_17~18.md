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


### 3-2. 위로 가기 버튼