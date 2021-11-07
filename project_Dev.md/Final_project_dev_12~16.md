# Final_Project_dev #.12 ~ 16 (10.30~11.3)

---

## 1. 여태 내가 한 일들 

- 백신 후유증으로 인해 11.1일까지 푹 쉬었다.
- 움직이는 이미지 카드폼 작성
- 화면 풀 스크린 구현 

<br />

## 2. 내일 내가 할 일

- 전반적인 코드 개선 및 사이드바 수정
- 데이터베이스에 필요한 이미지 및 음원 서치

<br />

## 3. 유용한 내용

이미지를 볼 때 좀 더 크게 확대해서 보고 싶은 생각에 어떤 방법이 있을지 궁금해서 찾아보게 되었다. 찾다 보니 리엑트에서 지원하는 fullsreen 라이브러리를 발견하게 되었고 실제로 이것을 적용해보니 너무 좋았다!! 사용방법은 아래와 같다!

```
npm i react-full-screen
```

설치부터 한다.

```js
import { FullScreen, useFullScreenHandle } from "react-full-screen";
```

설치 후 연결 해준다!

```js
import React, {useCallback} from 'react';
import { FullScreen, useFullScreenHandle } from "react-full-screen";

function App() {
  const handle = useFullScreenHandle();

  return (
    <div>
      <button onClick={handle.enter}>
        Enter fullscreen
      </button>

      <FullScreen handle={handle}>
        Any fullscreen content here
      </FullScreen>
    </div>
  );
}

export default App;
```

자세한 사항은 아래 링크를 통해!

![풀스크린 리엑트 라이브러리](https://www.npmjs.com/package/react-full-screen)




<br />

## 4. 마무리

백신 접종 후유증이 생각보다 오래 갔다... 거의 4일을 날려 먹어서 너무 속상하다... ㅠㅠ 그래서 그런지 뭔가 조급하게 코딩을 하는 것 같다... 내일 부터 다시 차분하게 진행 하도록 해야겠다! 내일은 전반적으로 코드를 수정하는 시간을 가질 것 같다! 