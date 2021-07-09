
### 액션함수만들기

```js
const ADD_TODO = "ADD_TODO"

function addTodo(todo){
    return {
        type: ADD_TODO,
        todo,
    }
}
```

### 리덕스의 리듀서
액션을 주면 그액션이 적용되어 달라진 결과를 만들어줌 
순수함수임 같은 인풋을 받으면 같은 결과를 

리듀서를 통해 스테이트가 달라졌음을 ㅇ리덕스가 인지하는 방식임
```js
function 리듀서(previousState, action){
    return newState;
}
```
액션을 받아서 스테이트를 리턴하는 구조
인자로 들어오는 previousState와 리턴되는 newState는 다른 참조를 가지도록해야됩니다.(이뮤터블)


```js
//아무 변화없을경우
//['코코','안녕']
function todoApp(previousState, action){
    //초기값을 설정해주는 부분
    if(previousState === undefined){
        return [];
    }

    if(action.type === ADD_TODO){
        return [...previousState, action.todo];
    }

    return previousState
}

//더쉬운 방법
const initialState = [];

function todoApp(previousState = initialState, action){
    // 생략 가능
    // if(previousState === undefined){
    //     return [];
    // }

    if(action.type === ADD_TODO){
        return [...previousState, action.todo];
    }

    return previousState
}
```

### 스토어 만들기

```js
const store = createStore(리듀서)

console.log(store) 
console.log(store.getSate()) //현재상태

store.dispatch(addTodo('coding')) //변경시켜주는함수
store.subscribe(()=>{})

```