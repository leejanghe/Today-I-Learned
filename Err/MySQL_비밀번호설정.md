## 비밀번호 에러 (ERROR 1045)

---

우선 `mysql -u root` 접속을 시도합니다.

```js
mysql -u root
```

```
ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: NO)
```

만약 위와 같은 에러가 뜨면 mysql에 접근하려면 비밀번호를 입력하라는 뜻입니다. 아래와 같이 입력합니다.

```js
// # -u(계정 접근), -p(비밀번호)
mysql -u root -p
```

초기에 설정한 비밀번호를 잘입력하면 실행이 잘되고 만약에 비밀번호가 기억이 안나면 아래와 같이 설정해서 접속할수있습니다.

```js
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'yourPassword';
```

위와같이 yourpassword에서 원하는 비밀번호를 설정하면 됩니다.
