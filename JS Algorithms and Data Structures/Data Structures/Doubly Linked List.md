# Doubly Linked List

```javascript

class Node {
    constructor(value) {
        this.value = value
        this.prev = null
        this.next = null
    }
}

class DoublyLinkList {
    head = null
    tail = null
    length = 0

    append(value) {
        const newNode = new Node(value)

        if (!this.head) {
            this.head = newNode
            this.tail = newNode
        } else {
            this.tail.next = newNode
            newNode.prev = this.tail
            this.tail = newNode
        }

        this.length++
        return this
    }

    prepend(value) {
        const newNode = new Node(value)

        if (!this.head) {
            this.head = newNode
            this.tail = newNode
        } else {
            this.head.prev = newNode
            newNode.next = this.head
            this.head = newNode
        }

        this.length++
        return this
    }

    insert(index, value) {
        if (index < 0 || index > this.length) throw new Error('Insert index out of bounds!')

        if (index === 0) {
            this.prepend(value)
            return this
        }
        if(index === this.length) {
            this.append(value)
            return this
        }

        const newNode = new Node(value)

        let nextNode = this.head
        for(let i = 0; i <= index - 1 ;i++) nextNode = nextNode.next
        const prevNode = nextNode.prev

        prevNode.next = newNode
        newNode.prev = prevNode
        newNode.next = nextNode
        nextNode.prev = newNode

        this.length++
        return this
    }

    remove(index) {
        if (index < 0 || index >= this.length) throw new Error('Remove index out of bounds!')

        if (this.length === 1) {
            this.head = null
            this.tail = null
        } else if (index === 0) {
            this.head = this.head.next
            this.head.prev = null
        } else if (index === this.length - 1) {
            this.tail = this.tail.prev
            this.tail.next = null
        } else{
            let curNode = this.head
            for(let i = 0; i <= index - 1 ;i++) curNode = curNode.next
            curNode.prev.next = curNode.next
            curNode.next.prev = curNode.prev 
        }

        this.length--
        return this
    }
}

```
