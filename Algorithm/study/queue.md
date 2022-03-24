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

## 문제예시
```js
class Node{
    constructor(value){
        this.value = value;
        this.next = null;
    }
}

class Queue{
    constructor(){
        this.head = null;
        this.tail = null;
    }

    enqueue(newValue){
        const newNode = new Node(newValue);
        if(this.head === null){
            this.head = this.tail = newNode;
        }else{
            this.tail.next = newNode;
            this.tail = newNode;
        }
    }

    dequeue(){
        const value =  this.head.value;
        this.head = this.head.next;
        return value;
    }

    peek(){
        return this.head.value;
    }
}


function solution(priorities, location){
    const queue = new Queue();
    for(let i=0; i<priorities.length; i++){
        queue.enqueue([priorities[i], i]);
    }
    priorities.sort((a,b)=>b-a);

    let count = 0;
    while(true){
        const currentValue = queue.peek();
        if(currentValue[0] < priorities[count]){
            queue.enqueue(queue.dequeue());
        }else{
            const value = queue.dequeue()
            count += 1;
            if(location === value[1]){
                return count
            }
        }
    }
    return count
}
```