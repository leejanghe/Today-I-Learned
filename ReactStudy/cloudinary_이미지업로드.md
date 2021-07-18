## Cloudinary

Cloudinary는 클라우드 기반 이미지 및 비디오 관리 서비스를 제공한다. 이를 통해 사용자는 웹 사이트 및 앱에 대한 이미지와 비디오를 업로드, 저장, 관리, 조작 및 전달할 수 있다.

---

### 이미지 업로드 기본 구조

아직 살펴봐야할 api문서가 많다. 자세한 사항은 [여기페이지](https://cloudinary.com/documentation/upload_images)참고해서 공부해야 겠다.

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