# mySQL 설치 및 삭제

이글은 맥os기준으로 작성된 글입니다. 완전히 삭제하고 다시 설치하는 방법 입니다.

---

## mySQL 완전히 삭제하기

### 설치가 잘되었는지 확인하는법

```js
mysql --version
```

### MYSQL 서비스 종류하기

```js
brew services stop mysql
```

### mySQL 삭제하기

```js
brew remove mysql
```

### 잔류파일 및 다른 파일 확실히 없애기

```js
brew cleanup
```

### 디렉토리 파일 확실히 없애기

```js
sudo rm -rf /user/local/var/mysql //비번치고 진행 비번설정 안했으면 그냥 엔터

// 아래 순서대로 진행
sudo rm -rf /user/local/mysql
sudo rm -rf /Library/StartupItem/MySQLCOM
sudo rm -rf /Library/PreferencePanes/MySql
```

하고 삭제 잘되었는지 확인하려면 `mysql --version` 치면 됩니다.

---

## mySQL 설치

### mySQL 설치하기

```js
brew install mysql
brew info mysql
```

### mySQL 실행하기

```js
brew services start mysql
mysql -u root -p
```

### mySQL 시작하기

```js
show databases;
```

```js
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
``` 

이게 나오면 잘 설치 되었습니다