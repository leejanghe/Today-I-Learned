## Middleware thunk

---

미들웨어 thunk함수 구조 알아보기

```js
function createThunkMiddleware(extraArgument){
    return({dispatch, getState}) => (next) => (action) => {
        // 구조분해 할당을 통해 스토어에서 dispatch와 getState 함수를 받아옵니다.
        if(typeof action === 'function') {
            // 액션객체가 아닌 함수가 액션으로 들어왔다면 받아온 dispatch를 함수의 인자로 넣어줍니다.
            return action(dispatch, getState, extraArgument);
        }
        // 액션객체가 들어왔다면 next를 통해 다음 미들웨어로 건내주거나 다음 미들웨어가 없다면 리듀서로 전달합니다.
        return next(action);
    }
}
//notify
export const notify = (message, dismissTime = 5000) => dispatch => {
    const uuid = Math.random()
    dispatch(enqueueNotification(message, dismissTime, uuid))
    //인자로 받아온 store.dispatch를 이곳에서 실행합니다. (액션객체 -> 리듀서)
    settimeout(()=>{
        dispatch(dequeueNotification())
    }, dismissTime)
    // 인자로 받아온 store.dispatch를 이곳에서 실행합니다. (액션객체 -> 리듀서)
}
```