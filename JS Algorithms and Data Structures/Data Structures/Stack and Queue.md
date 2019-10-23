# stack

### implement Stack.

```javascript

class Node {
  constructor(value){
    this.value = value
    this.next = null
  }
}

class Stack {
  constructor() {
    this.top = null
    this.length = 0
  }

  peek() {
    if (this.isEmpty()) {
      throw new Error('Stack is empty!')
    }
    return this.top.value
  }

  push(value) {
    const node = new Node(value)

    if(this.length === 0) {
      this.top = node
    } else {
      node.next = this.top
      this.top = node
    }

    this.length++
    return this
  }

  pop() {
    if (this.isEmpty()) {
      throw new Error('Stack is empty!')
    }

    const value = this.top.value
    this.top = this.top.next

    this.length--
    return value
  }
  
  isEmpty() {
    return this.length === 0
  }
}

const myStack = new Stack();

myStack.push('google')
myStack.push('baidu')
myStack.push('yahoo')

```

### Implement Queue using Stacks --- O(1)
```

/**
 * Initialize data structure here.
 */
const Queue = function() {
  this.input = new Stack()
  this.output = new Stack()
}

/**
 * Push element x to the back of queue. 
 * @param {number} x
 * @return {void}
 */
Queue.prototype.push = function(x) {
  this.input.push(x)
}

/**
 * Removes the element from in front of queue and returns that element.
 * @return {number}
 */
Queue.prototype.pop = function() {
  this.peek()
  return this.output.pop()
}

/**
 * Get the front element.
 * @return {number}
 */
Queue.prototype.peek = function() {
  if (this.empty()) throw new Error('Queue is empty!')

  if (this.output.isEmpty()) {
    while (!this.input.isEmpty()) {
      this.output.push(this.input.pop())
    }
  }
  return this.output.peek()
}

/**
 * Returns whether the queue is empty.
 * @return {boolean}
 */
Queue.prototype.empty = function() {
  return this.input.isEmpty() && this.output.isEmpty()
}

const myQueue = new Queue()

myQueue.push(1)
myQueue.push(2)
myQueue.push(3)

myQueue.peek() //1

myQueue.pop() // 1
myQueue.pop() // 2

myQueue.push(4)

myQueue.peek() // 3
myQueue.pop() // 3
myQueue.peek() // 4
myQueue.empty() // false

```