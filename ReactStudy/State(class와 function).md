## State (class형식)
요즘 함수형 프로그래밍은 useEffect를 import해서 사용하지만 레거시 형태도 알아볼 필요가 있습니다! 아래 구조가 레거시형으로 표현한 State관리법 입니다. state 객체로 초기값을 설정하고 어떤 함수를 변경해줄때 setState를 사용해서 변경하는 함수를 만듭니다. 이부분은 함수형과도 비슷하지만 큰차이점이 있다면 `this`의 유무입니다! 이점 꼭 알고 넘어갑시다!

```js
import React, { Component } from 'react'

class count extends Component {
    state = {
        count: 0,
    };

    handleIncrement = () => {
        this.setState({count: this.state.count +1})
    };
    handleDecrement = () => {
        const count = this.state.count -1
        this.setState({count: count < 0? 0:count}) //0 이하 출력 x
    };
    render() {
        return (
            <li>
            <span>count</span>
            <span>{this.state.count}</span>
            <button onClick={this.handleIncrement}>
                <i className="fas fa-plus-square"></i>
            </button>
            <button onClick={this.handleDecrement}>
                <i className="fas fa-minus-square"></i>
            </button>
            <button>
                <i className="fas fa-trash"></i>
            </button>
            </li>
        )
    }
}

export default count
```