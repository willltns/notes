# Graph

A graph data structure consists of a finite (and possibly mutable) set of **vertices** or nodes or points, together with a set of unordered **pairs** of these vertices for an undirected graph or a set if ordered pairs for a directed graph.

##### vertex & edge.
##### weighted & unweighted.
##### directed & undirected.

```javascript
// Simple implememtation. ignore some base errors & base cases.

class Graph {
    constructor() {
        this.adjacencyList = {} // hash table
    }

	/**
	 * @param vertex {string}
	 */
    addVertex(vertex) {
        this.adjacencyList[vertex] = []
    }

    addEdge(vert1, vert2) {
        this.adjacencyList[vert1].push(vert2)
        this.adjacencyList[vert2].push(vert1)
    }

    removeEdge(vert1, vert2) {
        this.adjacencyList[vert1] = this.adjacencyList[vert1].filter(v => v !== vert2)
        this.adjacencyList[vert2] = this.adjacencyList[vert2].filter(v => v !== vert1)
    }

    removeVertex(vertex) {
        this.adjacencyList[vertex].forEach(vert => this.removeEdge(vertex, vert))
        delete this.adjacencyList[vertex]
    }

    depthFirstTraverse_recursive(vertex) {
        const list = [], visited = {}, self = this

        !(function DFS(vertex) {
            visited[vertex] = true
            list.push(vertex)

            self.adjacencyList[vertex].forEach(neighbor => {
                if (visited[neighbor]) return

                DFS(neighbor)
            })
        }(vertex))
        
        return list
    }

    depthFirstTraverse_iterative(vertex) {
        const list = [], visited = {}
        const stack = [vertex]

        while (stack.length) {
            const vert = stack.pop()
            if (visited[vert]) continue

            visited[vert] = true
            list.push(vert)

            this.adjacencyList[vert].forEach(neighbor => {
                !visited[neighbor] && stack.push(neighbor)
            })
        }
        
        return list
    }

    breadthFirstTraverse(vertex) {
        const list = [], visited = {}
        const queue = [vertex]

        while (queue.length) {
            const vert = queue.shift()
            if (visited[vert]) continue

            visited[vert] = true
            list.push(vert)

            this.adjacencyList[vert].forEach(neighbor => {
                !visited[neighbor] && queue.push(neighbor)
            })
        }

        return list
    }
}

var g = new Graph()

g.addVertex('A')
g.addVertex('B')
g.addVertex('C')
g.addVertex('D')
g.addVertex('E')
g.addVertex('F')

g.addEdge('A', 'B')
g.addEdge('A', 'C')
g.addEdge('B', 'D')
g.addEdge('C', 'E')
g.addEdge('D', 'E')
g.addEdge('D', 'F')
g.addEdge('E', 'F')


//         A
//       /   \ 
//      B     C 
//      |     |
//      D ——— E
//       \   /
//         F

//   "A": [ "B", "C" ],
//   "B": [ "A", "D" ],
//   "C": [ "A", "E" ],
//   "D": [ "B", "E", "F" ],
//   "E": [ "C", "D", "F" ],
//   "F": [ "D", "E" ]
```