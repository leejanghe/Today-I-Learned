## DI(의존성 주입)

---

의존성 주입(Dependency Injection)은 객체가 필요로하는 어떤 객체를 생성자(Constructor) 혹은 새터(Setter)를 통해서 주입하는 것을 말합니다.

### DI의 장점

1. Unit Test가 용이해진다.
2. 코드의 재활용성을 높여준다.
3. 객체 간의 의존성(종속성)을 줄이거나 없엘 수 있다.
4. 객체 간의 결합도이 낮추면서 유연한 코드를 작성할 수 있다.


```js
class ImageUploader {
    async upload(file){
        const formData = new FormData();
        formData.append("file", file);
        formData.append("upload_preset", "docs_upload_example_us_preset");
        const result = await fetch(
            "https://api.cloudinary.com/v1_1/demo/image/upload",
            {
                method: 'POST',
                body: formData,
            }
        );
        return await result.json();
    }
}

export default ImageUploader
```

만약 위와 같은 클래스 객체를 다른 컴포넌트에 프롭스로 전달하고 싶을때 

```js
// index.js
//...생략
import AuthService from './service/auth_service';
import ImageUploader from './service/image_uploader';
import ImageFileInput from './components/image_file_input/image_file_input'

// DI
const authService = new AuthService();
const imageUploader = new ImageUploader();

// 아래와 같이 컴포넌트에 프롭스를 전달 이렇게 전달하면 조금 더 확장 가능한 컴포넌트가 됩니다.
const FileInput = props => (
<ImageFileInput {...props} imageUploader={imageUploader} />
);

ReactDOM.render(
  <React.StrictMode>
    <App authService={authService} FileInput={FileInput}/>
  </React.StrictMode>,
  document.getElementById('root')
);
```

index.js에서 프롭스를 자식들에게 전달하고 지정한 변수를 컴포넌트로 사용하면 됩니다.

```js
//....생략

머시기머시기({FileInput}){
  return (
    ...생략
    <FileInput />
  )
}
```