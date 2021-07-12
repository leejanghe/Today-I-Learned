## 1. 에러의 시작...

리엑트 개인작업을 하던 중 npm start를 입력했더니 `npm err! missing script: start` 오류가 발생했다. 검색을 통해서 package.json 파일에있는 스크립트 개체에 누락 되었고 누락 된 내용이 start명령 과 관련이 있음을 알게 되었습니다.


---

## 2. 해결 방법

먼저 터미널에 `npm inint`을 입력하면 package.json파일 만드는 과정이 나옵니다. 적절한 옵션을 선택 및 기입하고 Enter하고 넘어 갑니다! 그런 다음 package.json 파일에 들어갑니다!

```js
//package.json
{
  "name": "react-study",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "react-scripts start" // 여기부분!!!
  },
  "author": "",
  "license": "ISC",
  "description": ""
}
```

package.json 파일의 "scripts"개체에 start 스크립트를 추가 하고 다시 npm start를 하면 잘 해결 됩니다!!!

---

## 3. 정리

1. `npm err! missing script: start` 에러가 뜨면 script 개체에 start 스크립트가 없다!!
2. 터미널 창에 `npm init`을치고 package.json파일 기본 설정다하고 엔터!!
3. 새로 만든 package.json파일에서 "scripts"개체에 start 스크립트를 추가 하기
4. 저장 후 다시 터미널 창에 npm start