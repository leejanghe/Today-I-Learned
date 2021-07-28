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

모델 생성시 이름을 단수로 생성 합니다. (어차피 자동으로 복수형으로 나오게 합니다.)

```
npx sequelize-cli model:generate --name User --attributes firstName:string,lastName:string,email:string
```

위에 있는 명령문을 스프린트에서 요구하는 내용으로 변경하면 됩니다. 

```
npx sequelize-cli model:generate --name user --attributes url:string,title:string,visits:integer
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

## controllers 작성하기

내일정리