# shortly-MVC

---

# part1

## sequelize 설치

아래와 같이 sequelize설치합니다.

```
npm i --save sequelize
```

<br >

## sequelize-cli 설치

devDependencies에다 설치하는 이유는 개발환경에서만 진행하기 위함입니다.

```
npm i --save-dev sequelize-cli
```

<br >

## 빈프로잭트 만들기 (bootstraping)

실행하면 config/config.json, models/ ,migrations/ ,seeders/ 폴더들이 생깁니다.

<br >

```
npx sequelize-cli init
```

<br >

## MySQL 연결하기

mysql접속하기 위해 설정한 비밀번호와 config.json에서 비밀번호를 동일하게 합니다.  
또한 mysql에 접속해서 데이터베이스의 이름을 config.json에 있는 데이터베이스 이름을 같게해서 데이터베이스를 수동으로 만들어줍니다.

<br >

## 모델 만들기

모델 생성시 이름을 단수로 생성 합니다. (어차피 자동으로 복수형으로 나옵니다.)

```
npx sequelize-cli model:generate --name User --attributes firstName:string,lastName:string,email:string
```

위에 있는 명령문을 스프린트에서 요구하는 내용으로 변경하면 됩니다. 

```
npx sequelize-cli model:generate --name url --attributes url:string,title:string,visits:integer
```

<br >

## 마이그레이션 실행

마이그레이션은 데이터베이스 실제 디비에 심어주는 작업입니다. 데이터를 선택,준비, 추출 및 변환하는 작업을 합니다.

```
npx sequelize-cli db:migrate
```

<br >

## visits 초기값 설정

아래와 같이 visits를 객체로 담아 type과 defaultValue값을 설정할수 있습니다.

```js
//models/url.js
//...생략
 url.init({
    url: DataTypes.STRING,
    title: DataTypes.STRING,
    visits: {
      type: DataTypes.INTEGER,
      defaultValue:0
    }
  }, {
    sequelize,
    modelName: 'url',
  });
  //...생략
```

<br />

---

# part2

파트2를 진행하기 위한 간단한 수도 코드  

```js
//POST links 컨트룰러
1. URL을 포스트 요청으로 받습니다. //ex. {url:naver.com}

2. 요청에 있는 주소를 db에 레코드로 생성합니다.
2-1. url
2-2. url의 아이디
2-3. 홈페이지 제목
2-4. 방문횟수 -> 업테이트

3. 만약 이미 존해나는 url이면 그냥 넘어간다.

// get links/:id 컨트룰러
1. links/1 get 요청이 오면
2. id를 통해 레코드를 조회
3. 해당 레코드의 url을 컨트룰러에서 디다이렉트 시킴
4. 그리고 visits 필드 값을 1추가
```

## controllers 연결

테스트 케이스를 `'./controllers/links/index.js'` 보면 해당 폴더를 만들어서 index.js에서 로직을 작성합니다.

```js
describe('🚀 (2-1) controller 작성', () => {
  it('links controller 파일이 존재해야 합니다', () => {
    let hasLinksController = fs.existsSync('./controllers/links/index.js');
    expect(hasLinksController).to.be.true;
  });
```

<br />

## router 연결

```js
const express = require('express');
const router = express.Router();

//controller 가져오기
const controller = require('../controllers/links/index')

/* post link */
router.post('/', controller.post);

// get link
router.get('/', controller.get);

// get link /:id
router.get('/:id', controller.getId);


module.exports = router;
```

<br />

## controller 로직작성하기

```js
const models = require('../../models/index');
const {getUrlTitle} = require('../../modules/utils');
// const {url} = require('../../modules')

module.exports = {

    // get /link
    get: async (req, res)=>{
        //console.log('--------select문 조회',models.url.findAll())
        const urls = await models.url.findAll()
        res.status(200).json(urls)
    },

    // get /link/:id
    getId: async(req, res)=>{
        //console.log('-----------------',req.params)
        const id = req.params.id;
        const urlPk = await models.url.findByPk(id);
        await urlPk.increment('visits',{by:1})
        // console.log(urlPk)
        res.redirect(302, urlPk.url)
    },

    // post /link
    post:(req, res)=>{
       //console.log('----------------',req.body.url)
        const url = req.body.url;
        getUrlTitle(url, async(err, title)=>{
        const findUrl = await models.url.create({
            url,
            title
        });
        res.status(201).json(findUrl)
        })
    }
  }
  ```

  ## 최신화

  ```js
const models = require('../../models/index')
const {getUrlTitle,isValidUrl} = require('../../modules/utils')

const MU = models.url //어차피 계속 쓰게될테니 전역변수로 지정


// 모듈 구조분해 할당 팁
const 모듈 = {a:'안녕',b:'데이터정보'};
const {a:임의변수,b:나도변수} = 모듈

module.exports={
    get: async(req, res)=>{
        const urls = await MU.findAll()
        //console.log('----------------select조회',urls)
        res.status(200).json(urls)
    },


    getId: async(req, res)=>{
        const id = req.params.id;
        //console.log('---------------id값이 추가',req.params.id)
        const urlPk = await MU.findOne({where:{id}})

        // * 위에꺼 아래꺼 둘다 가능 개인적으로 주요키를 가져올땐 아래꺼 쓰는게 좋음
        //const urlPk = await MU.findByPk(id) 


        await urlPk.update({visits: urlPk.visits+1,})
        // * 인크리먼트도 가능 1씩 증가할때는 by:1 생략 가능
        //await urlPk.increment('visits',{by:1}) 

        res.redirect(302, urlPk.url)
    },



    post: async (req, res) => {
        const url = req.body.url;
        console.dir(url);
    
        // * url 유효성 검사
        if (!isValidUrl(url)) res.status(404).json({ message: "Invalid URL!" });
    
        getUrlTitle(url, async (err, title) => {
          //  * findOrCreate: 중복 검사
          const [result, created] = await MU.findOrCreate({
            where: { url },
            defaults: { title },
          });
          //  * 새로 추가한 경우
          if (created) res.status(201).json(result);
          //  * 기존 값이 있는 경우
          res.status(201).json(result);
        });
      }
    }
  ```

  이번 mvc 스프린트에서 가장 중요한점은 모델 데이터베이스 모듈을 가져와 컨트룰러에 연결시키는 작업이 중요하다. 아직 많이 어색하지만 자꾸 보면서 눈에 익히는게 중요할것 같다. 또 한 공식문서를 통해 실험 적용도 해봐야 겠다. 그리고 스프린트에서 테스트 케이스는 다 통과했지만 데이터가 중복으로 출력되는 현상, 초기값 null이 수정되지 않는 현상이 나타났다... 데이터 중복 출력 문제는 findOrCreate 함수를 사용해서 해결했지만 아직도 null은 해결하지 못했다... 실제 터미널로 작성해서 고치는 방법을 보았지만 와닿지 않는다...ㅠㅠ