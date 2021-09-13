# Oauth 스프린트

## 1. controller (callback)

```js
require('dotenv').config();

const clientID = process.env.GITHUB_CLIENT_ID;
const clientSecret = process.env.GITHUB_CLIENT_SECRET;
const axios = require('axios');

module.exports = (req, res) => {
  // req의 body로 authorization code가 들어옵니다. console.log를 통해 서버의 터미널창에서 확인해보세요!

  axios.post("https://github.com/login/oauth/access_token", {
    client_id: clientID,
    client_secret: clientSecret,
    code: req.body.authorizationCode
  },{headers:{
    accept:"application/json"
  }}).then(data => {
    // Github에서 스트링으로 주네???
    //console.log('@@#!@#!@#!@',data.data)
    // if(typeof(data.data) === "string"){
    //   const accessToken = data.data.split("&")[0].split("=")[1]
    //   console.log("파싱좀해줘",accessToken)
    //   return res.json({accessToken: accessToken})
    // }

    return res.json({
      accessToken: data.data.access_token
    })
  }).catch(err => {
    console.log("에러 발생")
  })

  // TODO : 이제 authorization code를 이용해 access token을 발급받기 위한 post 요청을 보냅니다. 다음 링크를 참고하세요.
  // https://docs.github.com/en/free-pro-team@latest/developers/apps/identifying-and-authorizing-users-for-github-apps#2-users-are-redirected-back-to-your-site-by-github

}
```

1. 콘솔로 req.body를 확인합니다.
2. 공식문서를 확인하고 필요한 값을 지정합니다. 이때 req.body안에 담긴 값은 authorizationCode 입니다. (중요포인트)
3. axios.post요청에서 3번째 인자값은 헤더옵션을 지정할수 있습니다. (지정 안하면 주석친 방법으로도 가능)

<br />

## 2. controller (images)

```js
const images = require('../resources/resources');

module.exports = (req, res) => {
  // TODO : Mypage로부터 access token을 제대로 받아온 것이 맞다면, resource server의 images를 클라이언트로 보내주세요.


  //console.log('@#!@#!@#!@#!@#!@#!@#!@#!@#!@',req.headers)
  const authorization = req.headers.authorization

if(!authorization){
  res.status(403).json({
    message:"no permission to access resources"
  });
}else{
  res.status(200).json({
    images
    });
  }
}
```

1. 콘솔로 req.headers 확인해보면 충분히 로직을 작성할수 있습니다.

<br />

# Client

## 1. login page

```js
class Login extends Component {
  constructor(props) {
    super(props)

    this.socialLoginHandler = this.socialLoginHandler.bind(this)

    // TODO: GitHub로부터 사용자 인증을 위해 GitHub로 이동해야 합니다. 적절한 URL을 입력하세요.
    // OAuth 인증이 완료되면 authorization code와 함께 callback url로 리디렉션 합니다.
    // 참고: https://docs.github.com/en/free-pro-team@latest/developers/apps/identifying-and-authorizing-users-for-github-apps

    this.GITHUB_LOGIN_URL = 'https://github.com/login/oauth/authorize?client_id={아이디값}}'
  }
```

깃에서 가져온 아이디(env파일에도 있음)를 url과 함께 작성해서 연결합니다.

<br />

## 2. mypage

```js

  async getGitHubUserInfo() {
    // TODO: GitHub API를 통해 사용자 정보를 받아오세요.
    // https://docs.github.com/en/free-pro-team@latest/rest/reference/users#get-the-authenticated-user

    
      let userInfoUrl = 'https://api.github.com/user'
      const res = await axios.get(userInfoUrl,{
        headers:{
          authorization: `token ${this.props.accessToken}`
        }
      })

    console.log('@@@@@@@@@@@',res.data)
    this.setState({
      userInfo:res.data
    })
  }

  async getImages() {
    // TODO : 마찬가지로 액세스 토큰을 이용해 local resource server에서 이미지들을 받아와 주세요.
    // resource 서버에 GET /images 로 요청하세요.
    let imageUrl = "http://localhost:8080/images"
    const res = await axios.get(imageUrl,{
      headers:{
        authorization: `token ${this.props.accessToken}`
      } 
    })
    this.setState({
      images:res.data.images
    })
  }
```