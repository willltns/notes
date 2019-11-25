# Max Binary Heap

```javascript
function MaxBinaryHeap() {
    this.heap = []
}

/**
 * Insert value. Bubble up.
 *
 * @param val {number}
 * @return val {number}
 */
MaxBinaryHeap.prototype.insert = function(val) {
    this.heap.push(val)

    let childIndex = this.heap.length - 1
    let parentIndex = Math.floor((childIndex - 1) / 2)

    if (childIndex === 0) return val

    while (this.heap[childIndex] > this.heap[parentIndex]) {
        // SWAP. (ES6)
        [ this.heap[childIndex], this.heap[parentIndex] ] = 
            [ this.heap[parentIndex], this.heap[childIndex] ]

        childIndex = parentIndex
        parentIndex = Math.floor((childIndex - 1) / 2)

        if (childIndex === 0) break
    }

    return val
}

/**
 * Extract max value, Sink down.
 *
 * @return max {number}
 */
MaxBinaryHeap.prototype.extractMax = function() {
    if (this.heap.length === 0) return undefined
    if (this.heap.length === 1) return this.heap.pop()

    const max = this.heap[0]
    this.heap[0] = this.heap.pop()

    let parentIndex = 0, leftChildIndex = 1, rightChildIndex = 2, maxChildIndex
    
    // If there's a left child, , try to compare and loop.
    while (leftChildIndex < this.heap.length) {
        // If right child not exsits.
        if (rightChildIndex >= this.heap.length) {
            // If parent is less than left child, make swap.
            if (this.heap[parentIndex] < this.heap[leftChildIndex]) {
                [ this.heap[parentIndex], this.heap[leftChildIndex] ] =
                    [ this.heap[leftChildIndex], this.heap[parentIndex] ]
            }
            // Finally break the loop.   
            break 
        }

        // If right child exsits, get the max child, 
        maxChildIndex = 
            this.heap[leftChildIndex] > this.heap[rightChildIndex]
                ? leftChildIndex
                : rightChildIndex
        
        // Then compare the max with parent, if parent is less than the max,
        // make swap and continue the loop, or else break.
        if (this.heap[parentIndex] < this.heap[maxChildIndex]) {
            [ this.heap[parentIndex], this.heap[maxChildIndex] ] =
                [ this.heap[maxChildIndex], this.heap[parentIndex] ]
        } else break

        parentIndex = maxChildIndex
        leftChildIndex = 2 * parentIndex + 1
        rightChildIndex = 2 * parentIndex + 2
    }

    return max
}

var m = new MaxBinaryHeap()
m.insert(55)
m.insert(67)
m.insert(11)
m.insert(33)
m.insert(101)
```
