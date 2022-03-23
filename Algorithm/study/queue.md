# Queue

큐는 first in first out이라는 개념을 가진 선형 자료구조다. 먼저 들어간것이 나중에 나오는 뜻이다. Liner Queue와 Circular Queue가 존재한다.

```js
// queue 코드
class Queue{
    constructor(){
        this.queue = [];
        this.front = 0;
        this.rear = 0;
    }

    enqueue(value){
        this.queue[this.rear++] = value;
    }

    dequeue(){
        const value = this.queue[this.front];
        delete this.queue[this.front]
        this.front += 1;
        return value
    }

    peek(){
        return this.queue[this.front];
    }
    
    size(){
        return this.rear - this.front;
    }
}

const queue = new Queue();
queue.enqueue(1);
queue.enqueue(2);
queue.enqueue(4);
console.log(queue.dequeue())  // 1
queue.enuqeue(8);
console.log(queue.size()); // 3
console.log(queue.peek()); // 2
console.log(queue.dequeue()) // 2
console.log(queue.dequeue()) // 4
```