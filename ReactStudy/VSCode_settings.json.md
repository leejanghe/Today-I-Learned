## VSCode 타이틀 바 세팅하기

---

VSCode에서 settings.json에서 VSCode 타이틀바 색상을 변경할수 있습니다! 안해도 상관 없지만 타이틀 바 색상을 변경 시켜 프로잭트의 중요도나 헷갈리지 않도록 할 수 있어서 유용한것 같습니다! 아래 코드를 복사해서 사용하길!!! 컬러 설정은 `#3F708D`을 바꿔서 원하는 색상으로 변경해서 사용하면 됩니다.

```js
//settings.js

{
    "workbench.colorCustomizations": {
    "titleBar.activeBackground": "#3F708D",
    "titleBar.inactiveBackground": "#3F708D"
    }
}
```
<br >


설정 전                      |  설정 후
:-------------------------:|:-------------------------:
![](./img/before.png)  |  ![](./img/after.png)

