# Singly Linked List

```javascript
class Node {
    constructor(value) {
        this.value = value
        this.next = null
    }
}

class LinkList {
    constructor() {
        this.head = null
        this.tail = null
        this.length = 0
    }

    getIndexPrevNode(index) {
        let nextNode = this.head
        for(let i = 0; i < this.length; i++) {
            if(i === index - 1) {
                return nextNode
            }
            nextNode = nextNode.next
        }
    }

    append(value) {
        const node = new Node(value)

        if (this.head === null) {
            this.head = node
            this.tail = node
        } else {
            this.tail.next = node
            this.tail = node
        }
        this.length++

        return this
    }

    prepend(value) {
        const node = new Node(value)

        if (this.head === null) {
            this.head = node
            this.tail = node
        } else {
            node.next = this.head
            this.head = node
        }
        this.length++
        return this
    }

    insert(index, value) {
        if (index < 0 || index > this.length) {
            throw new Error('Insert index out of bounds')
        }

        if (index === 0) {
            return this.prepend(value)
        }

        if (index === this.length) {
            return this.append(value)
        }

        const node = new Node(value)
        const prevNode = this.getIndexPrevNode(index)

        node.next = prevNode.next
        prevNode.next = node

        this.length++
        return this
    }

    remove(index) {
        if (index < 0 || index >= this.length) {
            throw new Error('Remove index out of bounds')
        }

        let value = null

        if (index === 0) {
            value = this.head.value
            this.head = this.head.next

            this.length === 1 && (this.tail = null)

            this.length--
            return value
        }
        
        const prevNode = this.getIndexPrevNode(index)
        if (index === this.length - 1) { 
            value = this.tail.value
            prevNode.next = null
            this.tail = prevNode
        }
        if (index > 0 && index < this.length - 1) {
            value = prevNode.next.value
            prevNode.next = prevNode.next.next
        }

        this.length--
        return value
    }

	reverse() {
        if (this.length === 1) return this

        let second = this.head.next
        this.head.next = null
        this.tail = this.head

        while(second) {
            const nextHead = second.next

            second.next = this.head
            this.head = second
            
            second = nextHead
        }
        return this
    }

}

const list = new LinkList()

list.append(1)
list.append(2)
list.append(5)

list.insert(1, 8)
list.insert(1, 28)
list.insert(5, 99)
list.insert(5, 999)
list.insert(0, 666)

list.insert(4, 44444)
list.insert(7, 77)

list.remove(3)
list.remove(0)
list.remove(6)

list.prepend(11)

list.insert(2, 22222)

list.remove(0)
list.remove(1)

console.log(list)

```