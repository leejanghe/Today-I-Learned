# Linux_사용권한과_환경변수 #2

---

## 환경변수에 대해 알아 볼 것

1. PC에 저장하는 환경변수가 무엇인지 어떻게 사용하는지
2. export, dotenv, .env에 대해 알아보기

---

## export

터미널에 명령어 export를 입력하면 기록된 환경 변수를 확인 할 수 있습니다. 변수를 설정할때는 등호 표시 앞뒤에는 반드시 공백이 없어야 합니다. (export는 많이 안씁니다. 간단하게 조회할때 사용)


## dotenv: 자바스크립트에서 환경변수 사용하기

dotenv쓰기 앞서 왜 쓰는지 이유를 알아야 합니다. 어떠한 규모있는 프로잭트를 진행 할때 API Key, 포트와 같이 공개할 수 없는 정보가 코드에 포함될 경우, 네트워크를 통해 API KEY가 노출될 경우가 있습니다. 깃 허브도 마찬가지 입니다. 그래서 이러한 중요한 정보 노출을 방지하고 보안을 위해 환경변수를 사용합니다.

```js
// dotenv 사용
npm init     // 엔터쳐서 설정 완료
npm i dotenv // 모듈설치
```

모듈을 설치하고 간단하게 index.js생성하고 `console.log(process.env)`를 입력하면 export로 확인한 내용과 동일한 내용을 객체로 출력합니다. 여기서 중요한 포인트는 `precess.env`는 노드 환경에서 조회가 가능하고 .env파일을 환경변수로 사용할 수 있게 도와줍니다. 

## .env: Node.js에서 환경변수 영구 적용

환경변수를 사용하는 방법은 간단합니다. 우선 .env파일을 생성하고 환경변수를 입력한 뒤 저장합니다.

```js
//환경변수 설정
nano .env  // 환경변수 설정하기
cat .env   // 환경변수 출력
```

CUI가 불편하면 그냥 .env파일을 만들어서 진행해도 상관 없습니다.

```js
//.env 파일
APIKEY = MY_API_KEY
```

.env파일에서 숨기고 싶은 정보를 변수로 담아서 저장합니다.

```js
//index.js
const dotenv = require('dotenv')
dotenv.config();
console.log(process.env.APIKEY)
```

위와 같이 dotenv모듈을 불러와서 .env파일과 같이 환경변수를 관리할수 있습니다.

```js
//터미널
node index.js // MY_API_KEY
```

아래 링크는 .env파일을 활용한 API 숨기기 예시입니다! 어떤식으로 사용하는 참고하면 좋을것 같습니다.<br />

[.env파일을 활용한 API키 숨기기](https://github.com/leejanghe/Today-I-Learned/blob/master/ReactStudy/api_%ED%82%A4_%EC%88%A8%EA%B8%B0%EA%B8%B0.md)

---

## 최종 정리

### 환경변수

환경변수는 개발자 개인의 API키나 기업용 API키 등 중요한 정보를 보호하기위한 변수입니다. 환경 변수를 활용하는 키워드는 export, dotenv, .env가 있습니다. export는 간단하게 환경변수를 조회할때 사용하고 dotenv는 자바스크립트 환경에서 사용하는 모듈로서 .env파일과 함께 환경 변수를 관리합니다.