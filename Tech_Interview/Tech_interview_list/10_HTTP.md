## CORS란 무엇이고 목적은 어떻게 되는지 설명해주세요. 그리고 노드JS 기반의 웹 서버에서 CORS를 어떻게 설정하는지 설명해주세요.

---

### CORS란 ?
Cross-Origin-Sharing은 추가적인 HTTP header를 사용해서 실행중인 웹이 다른 origin의 리소스에 접근할 수 있도록 하는 메커니즘을 의미한다.

<br />

### 왜 필요한가요 ?
기본적으로 브라우저는 Same-origin policy 동일출처정책을 따른다. 따라서 API요청시 이정책에 따라 동일한 출처의 리소스만을 요청할 수 있습니다. 하지만 웹 어플리케이션을 구현하다보면, 다른 출처제 있는 리소스를 요청해야하는 경우가 많습니다. 이를 안전하게 처리할 정책인 cross-origin 요청을 제한적으로 허용합니다.

<br />

### 어떻게 구성되고 어떻게 동작하는가 ?
브라우저는 출처가 다른 요청을 보낼때 Access-Control-Allow-Origin 이라는 헤더를 추가한다 만약 리소스에도 동일한 Access-Control-Allow-Origin 정보가 등록된 상태라면 안전한 요청으로 간주하고 응답데이터를 준다.

<br />

### NodeJS 기반의 웹 서버에서 CORS를 어떻게 설정하는가 ?
NodeJS에서 Cors를 설정하려면 응답헤더에 각각 정보를 담아주어야해서 번거롭다. 하지만 Access-Control-Allow-Origin헤더를 설정해줄 수 있는 cors npm 모듈을 이용하면 편리하게 설정이 가능하다. 방법은 cors()안에 origin credentials, methods 정보를 객체형태로 담아주면 됩니다.