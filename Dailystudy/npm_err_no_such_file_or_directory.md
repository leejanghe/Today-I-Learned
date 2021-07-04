## 1. Error: ENOENT: no such file or directory

전에는 잘됬는데 왜 안되지 ?ㅡㅡ 코린이 입장에서는 너무 당혹 스러운일...하지만 이문제는 대부분 파일 경로를 잘못 불러와서 일어난 에러일 가능성이 크다! 이런 에러를 보았을 때는 꼭 폴더 루트를 잘 확인해보자!!!


---

## 2. 추가적으로 로그가 쌓여서 안되는 경우 
<br />

1. 캐시정리
```js
npm cache clean --force
```
<br />

2. 기존 파일 삭제 : node_modules, package-lock.json
```js
rm -rf ./node_modules
rm -rf ./package-lock.json
```
<br >

3. npm 재설치
```js
npm i
```

4. `npm start`
