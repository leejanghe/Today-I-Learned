## 이미지 업로드하기

파일업로드시 e.target.files 라는 코드를 활용하면 업로드한 파일을 리스트로 알려줍니다. 그리고 Url.createObjectURL()여기다 업로드한 파일을 담으면 가상의 url을 하나 생성해줍니다. 이떄 이 url을 활용해서 이미지 태그에 넣으면 됩니다.

```js
//... 생략
methods : {
upload(e){
      let uploadImg = e.target.files;
      console.log('1', uploadImg[0])
      let url = URL.createObjectURL(uploadImg[0]);
      console.log('2',url)
      this.upLoadUrl = url;
      this.step++;
    },
}
```

여기서 this.step은 다음 단계로 넘어가기 위한 코드입니다. 그리고 html에서 @change에 위에 만들었던 upload함수를 넣어 줍니다.

```html
<input @change="upload" accept="image/*" type="file" id="file" class="inputfile" />
<label for="file" class="input-plus">+</label>
```

여기서 accetp 속성을 활용해서 파일을 제한 할 수 있습니다.