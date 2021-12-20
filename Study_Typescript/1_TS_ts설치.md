## 타입스크립트를 쓰는 이유

타입스크립트는 자바스크립트의 타입부분을 업그레이드해서 사용하고 싶을 때 설치해서 쓰는 일종의 자바스크립트 대용품입니다. 그냥 자바스크립트 문법 그대로 이용하나 엄청 엄격한 언어라고 생각하면 됩니다. 타입스크립트를 쓰는 이유는 자바스크립트의 타입이 워낙 관대해서 타입관련된 버그들이 많이 생겨 납니다. 그래서 이러한 에러를 확실히 잡고 정확하게 코드를 작성하기 위해 타입 스크립트를 사용합니다.

<br />

## 타입스크립트 설치

아래와 같이 설치를 해줍니다 에러가 날경우 노드js를 최신버전으로 설치하거나 터밀널창에 sudo를 붙여서 설치합니다.

```js
$ npm install -g typescript
```

<br />

## tsconfig.json 파일 만들기

타입스크립트 ts파일들을 .js파일로 변환할 때 어떻게 변환할 것인지 설정하는 기능입니다.

```js
{
    "compilerOptions": {
        "target": "es5",
        "module": "commonjs",
    }
}
```

<br />

## 파일명은 .ts만들기 & tsc -w입력하기

파일명은 .ts를 붙여서 사용합니다 그리고 터미널에 tsc -w 입력하면 자동으로 ts파을을 js파일로 변환해줍니다.

```js
$ tsc -w
```

<br />

---

## 리엑트에서 ts설치하기

1. 이미 작업 중에 있는 React 프로젝트에 설치하는 경우

```js
npm install --save typescript @types/node @types/react @types/react-dom @types/jest
```

<br />

2. 새로운 React 프로젝트를 만드는 경우

```js
npx create-react-app my-app --template typescript
```