## VS code git 5k 삭제 방법

```
git rev-parse --show-toplevel
```

이명령어를 쳐서 root repository를 알수 있다. 그다음

```
ls -a
```

전체 목록을 조회하고 .git이라는 파일이 있을 것이다.

```
rm -r -f .git
```

위와 같이 치면 VS code 5k 에러를 해결 할 수 있다. 주의 할점은 git clean -f -d는 함부로 치지말자!

[참고](https://seanlion.github.io/blog/25)