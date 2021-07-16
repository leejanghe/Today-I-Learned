## swiper

[swiper](https://swiperjs.com/demos)사이트는 정말 유용한 것 같다. 프로잭트 렌딩페이지 구현 할때 꼭 참고해서 사용하면 괜찮을 것 같다!

```js
import React, { useRef, useState } from "react";
// Import Swiper React components
import { Swiper, SwiperSlide } from "swiper/react";

// Import Swiper styles
import "swiper/swiper.min.css";
import "swiper/components/scrollbar/scrollbar.min.css"

import "./styles.css";


// import Swiper core and required modules
import SwiperCore, {
  Scrollbar
} from 'swiper/core';

// install Swiper modules
SwiperCore.use([Scrollbar]);


export default function App() {
  
  
  
  return (
    <>
    <Swiper scrollbar={{
  "hide": true
}} className="mySwiper">
  <SwiperSlide>Slide 1</SwiperSlide>
  <SwiperSlide>Slide 2</SwiperSlide>
  <SwiperSlide>Slide 3</SwiperSlide>
  <SwiperSlide>Slide 4</SwiperSlide>
  <SwiperSlide>Slide 5</SwiperSlide>
  <SwiperSlide>Slide 6</SwiperSlide>
  <SwiperSlide>Slide 7</SwiperSlide>
  <SwiperSlide>Slide 8</SwiperSlide>
  <SwiperSlide>Slide 9</SwiperSlide>
  </Swiper>
    </>
  )
}
```