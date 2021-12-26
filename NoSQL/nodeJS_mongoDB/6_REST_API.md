## API란

Application Programming interface 약자로 서로 다른 프로그램간에 소통할 수 있게 도와주는 통신 규약을 뜻합니다. 즉 서버에게 요청해서 데이터 가져오는 방법이 API입니다.

<br />

## REST API

Representational State Transfer 뜻으로 API 디자인 방법입니다. REST API에는 6가지 원칙이 있습니다.  

1. Uniform interface  
- 하나의 URL로는 하나의 데이터를 가져와야하고 간결하고 예측가능해야 합니다.  

2. Client-server 역할 구분하기
- URL 하나만 알면 서버에 있는 자료를 쓸수 있어야 합니다.  

3. Stateless
- 요청들은 각각 독립적으로 처리되어야 합니다.  

4. Cacheable
- 요청을 통해 보내는 자료들은 캐싱이 가능해야 합니다.  

5. Layered System
- 여러가지 단계를 거쳐서 요청을 처리해야 합니다.  

6. code on Demand
- 서버는 고객에게 실제 실행가능한 코드를 전송해줄 수도 있습니다.  