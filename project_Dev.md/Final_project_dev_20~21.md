# Final_Project_dev #.20 ~ 21 (11.8 ~ 11.9)

---

## 1. 여태 내가 한 일들 

- 터치 페이지 css작업 보완
- 찜 목록 페이지 css작업 보완
- 찜 목록 페이지 삭제 구현
- 터치 페이지 재싱 및 정지 기능 구현

<br />

## 2. 내일 내가 할 일

- 마이페이지 css 최종 보완
- 메인 홈 페이지 css 보완

<br />

## 3. 유용한 내용

useRef를 활용해서 오디오를 제어 할 수 있었다. 재생 및 정지 헨들 함수를 만들어서 제어 할 해당 오디오에 ref를 념겨주면 끝이다. 생각 보다 간단해서 좋았다. 이에 해당하는 간단한 로직은 아래와 같다.

```js
//...생략

 const audioRef = useRef(null);
      
 const handlePlay = () => {
       audioRef.current.play();
        };
      
 const handlePause = () => {
       audioRef.current.pause();
        };
//... 생략

<button onClick={handlePlay}>재생</button>
<button onClick={handlePause}>중지</button>
<button onClick={handle.enter}>Enter fullscreen</button>
<button onClick={handleLikeCardClick}>찜하기 입니당</button>
<audio 
autoPlay='autoPlay'
ref={audioRef} src={moveImgs.sound} type="audio/mpeg" ></audio>

```

<br />

## 4. 마무리..

거의 마무리 단계여서 css작업만 주먹구구로 하고 있다... 생각 보다 오래 걸린다... 오늘 무슨일이 있어도 꼭 완료 해야 된다... 밤세자...