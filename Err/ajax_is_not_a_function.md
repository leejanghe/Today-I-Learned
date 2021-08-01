## Uncaught TypeError: $.ajax is not a function

ajax 요청을 하기 위해선 jQuery를 설치해서 사용해야 한다. 사용하다 보면 아래와 같은 에러가 종종 뜨곤 한다.

```js
Uncaught TypeError: $.ajax is not a function
at HTMLButtonElement.<anonymous> (list:59)
at HTMLButtonElement.dispatch (jquery-3.4.1.min.js:2)
at HTMLButtonElement.v.handle (jquery-3.4.1.min.js:2)
```

이러한 에러가 뜨는 이유는 아래와 같다

```
The issue here is that the Slim version of JQuery doesn’t support Ajax. 
```

제이쿼리의 Slim 버전은 Ajax를 지원하지 않기떄문이다. 그래서 스크립트에서 slim 부분을 삭제하면 해결이 됩니다.

```js
// slim버전은 ajax가 지원이 안됩니다
<script src="https://code.jquery.com/jquery-3.4.1.slim.min.js"></script>

// 아래와 같이 바꿔주면 해결이 됩니다.
<script src="https://code.jquery.com/jquery-3.4.1.min.js"></script>
```