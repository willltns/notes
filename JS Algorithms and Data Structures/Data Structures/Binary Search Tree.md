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






    // First version of remove method implementation. something different, something may wrong.
    firstVersionRemove(value) {
        let curNode = this.root, parentNode = null

        if (!this.root) return false

        // Match root node
        if (value === curNode.value) {

            if (!curNode.left && !curNode.right) this.root = null

            else if (curNode.left && !curNode.right) this.root = curNode.left

            else if (!curNode.left && curNode.right) this.root = curNode.right

            else if (curNode.left && curNode.right) {
                let rightMin = curNode.right, rightMinParent = curNode
                while (rightMin.left) {
                    rightMinParent = rightMin
                    rightMin = rightMin.left
                }

                this.root = rightMin

                rightMinParent.left = rightMin.right

                rightMin.left = curNode.left
                rightMin.right = curNode.right
            }
            return true
        }

        while (curNode) {
            // To right.
            if (value > curNode.value) {
                if (!curNode.right) return false

                parentNode = curNode
                curNode = curNode.right
                // Match and remove right node.
                if (value === curNode.value) {
                    if (!curNode.left && !curNode.right) parentNode.right = null

                    else if (curNode.left && !curNode.right) parentNode.right = curNode.left

                    else if (!curNode.left && curNode.right) parentNode.right = curNode.right

                    else if (curNode.left && curNode.right) {
                        let rightMin = curNode.right, rightMinParent = curNode
                        while (rightMin.left) {
                            rightMinParent = rightMin
                            rightMin = rightMin.left
                        }

                        parentNode.right = rightMin

                        if (rightMin !== curNode.right) {
                            rightMinParent.left = rightMin.right
                            rightMin.right = curNode.right
                        }
                        rightMin.left = curNode.left
                    }
                    return true
                }
            // To left.
            } else if (value < curNode.value) {
                if (!curNode.left) return false

                parentNode = curNode
                curNode = curNode.left
                // Match and remove left node.
                if (value === curNode.value) {
                    if (!curNode.left && !curNode.right) parentNode.left = null

                    else if (curNode.left && !curNode.right) parentNode.left = curNode.left

                    else if (!curNode.left && curNode.right) parentNode.left = curNode.right

                    else if (curNode.left && curNode.right) {
                        let rightMin = curNode.right, rightMinParent = curNode
                        while (rightMin.left) {
                            rightMinParent = rightMin
                            rightMin = rightMin.left
                        }
                        
                        parentNode.left = rightMin

                        if (rightMin !== curNode.right) {
                            rightMinParent.left = rightMin.right
                            rightMin.right = curNode.right
                        }
                        rightMin.left = curNode.left
                    }
                    return true
                }
            }
        }
        return false
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
