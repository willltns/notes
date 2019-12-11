# Dijkstra's Algorithm

An algorithm for finding the shortest paths between nodes in a graph.

```javascript

class PriorityQueue {
    /**
     * Initialize the queue
     */
    constructor() {
        this.queue = []
    }
    
    /**
     * Get the size of the queue
     */
    size() {
      return this.queue.length
    }
    
    /**
     * Enqueue node. then sort by bubble up.
     *
     * @param value {any}
     * @param priority {number}
     * @return node {object}
     */
    enqueue(value, priority) {
        const node = { value, priority }
        this.queue.push(node)

        let childIndex = this.queue.length - 1
        let parentIndex = Math.floor((childIndex - 1) / 2)

        if (childIndex === 0) return node

        while (this.queue[parentIndex].priority > this.queue[childIndex].priority) {
            // SWAP. (ES6)
            [ this.queue[childIndex], this.queue[parentIndex] ] = 
                [ this.queue[parentIndex], this.queue[childIndex] ]

            childIndex = parentIndex
            parentIndex = Math.floor((childIndex - 1) / 2)

            if (childIndex === 0) break
        }

        return node
    }

    /**
     * Dequeue priority node, then sort by sink down.
     *
     * @return node {object}
     */
    dequeue() {
        if (this.queue.length === 0) return undefined
        if (this.queue.length === 1) return this.queue.pop()

        const priority = this.queue[0]
        this.queue[0] = this.queue.pop()

        let parentIndex = 0, leftChildIndex = 1, rightChildIndex = 2, priorityChildIndex

        // If there's a left child, try to compare and loop.
        while (leftChildIndex < this.queue.length) {
            // If right child not exsits.
            if (rightChildIndex >= this.queue.length) {
                // If parent has less priority over child, make swap.
                if (this.queue[parentIndex].priority > this.queue[leftChildIndex].priority) {
                    [ this.queue[parentIndex], this.queue[leftChildIndex] ] =
                        [ this.queue[leftChildIndex], this.queue[parentIndex] ]
                }
                // Finally break the loop.   
                break 
            }

            // If right child exsits, compared with left child, and get the priority child, 
            priorityChildIndex = 
                this.queue[leftChildIndex].priority < this.queue[rightChildIndex].priority
                    ? leftChildIndex
                    : rightChildIndex

            // Then compare the priority child with parent, If parent has less priority over child,
            // make swap and continue the loop, or else break.
            if (this.queue[parentIndex].priority > this.queue[priorityChildIndex].priority) {
                [ this.queue[parentIndex], this.queue[priorityChildIndex] ] =
                    [ this.queue[priorityChildIndex], this.queue[parentIndex] ]
            } else break

            parentIndex = priorityChildIndex
            leftChildIndex = 2 * parentIndex + 1
            rightChildIndex = 2 * parentIndex + 2
        }

        return priority
    }
}

class WeightedGraph {
    constructor() {
        this.adjacencyList = {}
    }

    /**
     * add vertex
     *
     * @param vertex {string}
     */
    addVertex(vertex) {
        this.adjacencyList[vertex] = []
    }
    
    /**
     * add weighted connection between two vertexes.
     *
     * @param vertex1 {string}
     * @param vertex2 {string}
     * @param weight {number}
     */
    addEdge(vertex1, vertex2, weight) {
        this.adjacencyList[vertex1].push({ node: vertex2, weight })
        this.adjacencyList[vertex2].push({ node: vertex1, weight })
    }

    // ...

    /**
     * Find the shortest distance from start to end.
     *
     * @param start {string}  eg. A
     * @param end {string}  eg. C
     * @return result {string}  eg. A -> B -> C
     */
    Dijkstra(start, end) {
        const pq = new PriorityQueue(), distances = {}, paths = {}, result = []

        // Initialize and prepare state before computing.
        for (let vertex in this.adjacencyList) {
            if (vertex === start) {
                pq.enqueue(vertex, 0)
                distances[vertex] = 0
            } else {
                pq.enqueue(vertex, Infinity)
                distances[vertex] = Infinity
            }
        }

        let minVertex, neighborVertex, neighborDistance

        while (pq.size()) {
            minVertex = pq.dequeue().value

            // Get the shortest path to the end.
            if (minVertex === end) {
                result.push(minVertex)

                let previous = paths[minVertex]
                while (previous) {
                    result.push(previous)
                    previous = paths[previous]
                }

                break
            }
            
            // Compute the distance from start to each next neighbor.
            this.adjacencyList[minVertex].forEach(neighbor => {
                neighborVertex =  neighbor.node
                neighborDistance = distances[minVertex] + neighbor.weight

                // If the distance is shorter than previous, update and record, or else pass.
                if (neighborDistance < distances[neighborVertex]) {
                     distances[neighborVertex] = neighborDistance
                     paths[neighborVertex] = minVertex
                     pq.enqueue(neighborVertex, neighborDistance)
                }
            })
        }

        return result.reverse().join(' -> ')
    }
}

var graph = new WeightedGraph()
graph.addVertex('A');
graph.addVertex('B');
graph.addVertex('C');
graph.addVertex('D');
graph.addVertex('E');
graph.addVertex('F');

graph.addEdge('A', 'B', 4);
graph.addEdge('A', 'C', 2);
graph.addEdge('B', 'E', 3);
graph.addEdge('C', 'D', 2);
graph.addEdge('C', 'F', 4);
graph.addEdge('D', 'E', 3);
graph.addEdge('D', 'F', 1);
graph.addEdge('E', 'F', 1);


graph.Dijkstra('A', 'E');

// ['A', 'C', 'D', 'F', 'E']

```