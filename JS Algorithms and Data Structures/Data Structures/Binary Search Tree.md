# Binary Search Tree

```javascript

class Node {
    constructor(value) {
        this.value = value
        this.left = null
        this.right = null
    }
}

class BinarySearchTree {
    root = null

    insert(value) {
        const newNode = new Node(value)

        let parentNode = this.root
        while (parentNode) {
            // To right
            if (newNode.value > parentNode.value) {
                if (!parentNode.right) {
                    parentNode.right = newNode
                    break
                }
                parentNode = parentNode.right
            // To left
            } else {
                if (!parentNode.left) {
                    parentNode.left = newNode
                    break
                }
                parentNode = parentNode.left
            }
        }

        if (!this.root) this.root = newNode

        return this
    }

    lookup(value) {
        let parentNode = this.root
        while (parentNode) {
            if (value > parentNode.value) {
                parentNode = parentNode.right
            } else if (value < parentNode.value) {
                parentNode = parentNode.left
            } else if (value === parentNode.value) {
                return parentNode
            }
        }

        return false
    }

    getAdjustedSubTree(curNode) {
        // curNode doesn't have a right child, return left child.
        if (!curNode.right) return curNode.left

        // or curNode has a right child,
        // then find right subtree's min node and replace.
        let rightMin = curNode.right, rightMinParent = curNode
        while (rightMin.left) {
            rightMinParent = rightMin
            rightMin = rightMin.left
        }
        // curNode's right child has left child.
        if (rightMin !== curNode.right) {
            rightMinParent.left = rightMin.right
            rightMin.right = curNode.right
        }
        rightMin.left = curNode.left

        return rightMin
    }

    remove(value) {
        if (!this.root) return false

        let curNode = this.root, parentNode = null
        // Match the root node
        if (value === curNode.value) {
            this.root = this.getAdjustedSubTree(curNode)
            return true
        }

        while (curNode) {
            // To right.
            if (value > curNode.value) {
                if (!curNode.right) return false

                parentNode = curNode
                curNode = curNode.right
                // Match and replace right child.
                if (value === curNode.value) {
                    parentNode.right = this.getAdjustedSubTree(curNode)
                    return true
                }
            // To left.
            } else if (value < curNode.value) {
                if (!curNode.left) return false
                
                parentNode = curNode
                curNode = curNode.left
                // Match and replace left child.
                if (value === curNode.value) {
                    parentNode.left = this.getAdjustedSubTree(curNode)
                    return true
                }
            }
        }
        return false
    }

    breadthFirstTraverse_iterative() {
        if (this.root === null) return
        
        const queue = [this.root], list = []

        while(queue.length) {
            const curNode = queue.shift()
            list.push(curNode.value)

            if (curNode.left) queue.push(curNode.left)
            if (curNode.right) queue.push(curNode.right)
        }

        return list
    }

    breadthFirstTraverse_recursive(queue = [this.root], list = []) {
        if (queue.length === 0) return list

        const curNode = queue.shift()
        list.push(curNode.value)

        if (curNode.left) queue.push(curNode.left)
        if (curNode.right) queue.push(curNode.right)

        return this.breadthFirstTraverse_recursive(queue, list)
    }

    DFSInOrder() {
        const data = []
        function traverse(node) {
            if (node.left) traverse(node.left)
            data.push(node.value)
            if (node.right) traverse(node.right)
        }

        traverse(this.root)
        return data
    }

    DFSPreOrder() {
        const data = []
        function traverse(node) {
            data.push(node.value)
            if (node.left) traverse(node.left)
            if (node.right) traverse(node.right)
        }
        
        traverse(this.root)
        return data
    }

    DFSPostOrder() {
        const data = []
        function traverse(node) {
            if (node.left) traverse(node.left)
            if (node.right) traverse(node.right)
            data.push(node.value)
        }
        
        traverse(this.root)
        return data
    }
}

var tree = new BinarySearchTree()

tree.insert(100)
tree.insert(66)
tree.insert(55)
tree.insert(77)
tree.insert(150)
tree.insert(120)
tree.insert(110)
tree.insert(130)

tree.insert(125)
tree.insert(127)

```
