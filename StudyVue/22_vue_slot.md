## slot문법

자식이 부모데이터를 사용하고 싶을때 사용합니다. 다만 프롭스는 src, style속성에서도 사용가능하지만 slot은 html태그이기 떄문에 html태그처럼만 사용이 가능합니다.

<br />

### 1. 자식 컴포넌트

<slot></slot>태그를 이용해서 데이터를 표시할 곳을 정합니다.

```html
<div :class="filterData + ' filter-item'" :style="`background-image:url(${upLoadUrl})`">
      <slot></slot>
</div>
```

<br />

### 2. 부모 컴포넌트

부모는 <자식컴포넌트>데이터</자식컴포넌트> 이렇게 자식컴포넌트 사이에 데이터를 작성해서 보냅니다.

```html
<FilterBox :filterData= "filterData[i]" :upLoadUrl= "upLoadUrl" v-for="(a,i) in filterData" :key="i">
      {{filterData[i]}}
</FilterBox>
```