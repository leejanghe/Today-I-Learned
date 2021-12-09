## CSSgram

cssgram은 css속성만으로 인스타 필터들을 흉내낼수 있는 라이브러리 입니다. 사용법은 간단합니다. 그냥 원하는 이미지에 클래스에 공식 필터명을 작성하면 됩니다.

<br />

### cdn 설치

cdn 방식으로 첨부된 링크태그를 index.html에 넣습니다.

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/cssgram/0.1.12/cssgram.min.css" integrity="sha512-kr3JaEexN5V5Br47Lbg4B548Db46ulHRGGwvyZMVjnghW1BKmqIjgEgVHV8D7V+Cbqm/VBgo3Rcbtv+mGLoWXA==" crossorigin="anonymous" /> 
```

<br />

### 데이터 저장

인스타 그램 필터 클래스명을 데이터에 저장합니다.

```js
data(){
        return {
            filterData : [ "aden", "_1977", "brannan", "brooklyn", "clarendon", "earlybird", "gingham", "hudson", 
"inkwell", "kelvin", "lark", "lofi", "maven", "mayfair", "moon", "nashville", "perpetua", 
"reyes", "rise", "slumber", "stinson", "toaster", "valencia", "walden", "willow", "xpro2"]
        }
    },
```

<br />

### 데이터 쓰기

저장된 데이터를 바인딩해서 사용하면 끝

```html
<FilterBox :filterData= "filterData[i]" :upLoadUrl= "upLoadUrl" v-for="(a,i) in filterData" :key="i"> </FilterBox>
```

