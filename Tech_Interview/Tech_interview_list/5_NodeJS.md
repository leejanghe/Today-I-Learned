## 노드js는 싱글스레드 인가요 ? 노드 js런타임이 동작하는 방식을 설명해주세요!

- 자바스크립트 -> 싱글스레드 랭귀지 : 코드를 한번에 하나밖에 실행하지 못함
- 노드js -> 자바스크립트를 브라우저 밖에서도 실행 할 수 있도록 하는 자바스크립트 런타임

<br />

- 콜스택과 태스크 큐
자바스크립트 엔진은 요청이 들어올 때마다 요청을 순차적으로 call stack에 담아 하나씩 처리한다. call stack은 하나만 존재하기 때문에 요청도 하나씩만 처리할 수 밖에 없다. task queue는 처리해야 하는 task를 임시로 저장해두는 큐다. call stack이 비워지면 task queue에 있던 task들이 순서대로 call stack에 push된다.

<br />

- Node.js는 싱글스레드! 프로세스 내에서 하나의 스레드가 하나의 요청만을 수행함. 한번에 여러 요청을 수행할 수 없음 → 블로킹 모델

- 또한 클러스터링을 통해 프로세스를 포크하여 멀티스레드인것처럼 사용가능
- 싱글스레드이지만 완전한 싱글 스레드를 기반으로 동작하지는 않음. 일부 작업들은 libuv의 스레드 풀에서 수행되기 때문. libuv 라이브러리가 이벤트기반, 논블로킹 I/O를 구현함
- 특징 → 이벤트 기반, 논블로킹 I/O 모델
- Node JS의 특성인 이벤트 기반, 논블로킹 I/O 모델들은 모두 libuv 라이브러리에서 구현됨