## jwt

우선 터미널 창에서 `npm i jsonwebtoken`을 설치합니다.

```js
import jwt from 'jsonwebtoken';

const secret = 'dfefadfjasdflkd'
const token = jwt.sign({
    id:'joycoding',
    isAdmin:false,
},
secret,
{expiresIn:2}
);

jwt.verify(token, secret, (err,decoded)=>{
    console.log(err, decoded)
})


console.log(token)
```

jwt.sign({정보, 해시솔트값, {옵션}})  
jwt.verify(토큰,해시,(콜백))