## MySQL_삭제 및 설치

아래 명령어를 순서대로 실행하면 삭제 및 설치를 할수 있습니다.

```js
// MySQL 삭제
brew services stop mysql
brew remove mysql
brew cleanup

// 권한으로 잔류 파일 삭제
sudo rm -rf /usr/local/mysql
sudo rm -rf /Library/StartupItems/MySQLCOM
sudo rm -rf /Library/PreferencePanes/MySql


// 다시 설치
brew install mysql
brew services start mysql
mysql -u root -p
```