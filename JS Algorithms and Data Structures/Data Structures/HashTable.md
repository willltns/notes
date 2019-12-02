# HashTable
Hash Tables are collections used to store *key-value* pairs. and are fast for finding values, adding new values, and removing values.

**Big O:** (average case)
- insertion -> **O(1)**
- deletion -> **O(1)**
- access -> **O(1)**

## Hash Function
- fast
- uniformly & evenly distribution
- and deterministic (same input yields same output)

#### Hash Function Implementation
```javascript
// base hash function implementation.
function hash(key, arrLength) {
    let total = 0
    // Prime number is helpful in distributing data uniformly.
    let WEIRD_PRIME = 31
    
    for (let i = 0; i < Math.min(key.length, 30); i++) {
    	let char = key[i]
    	let value = char.charCodeAt(0) - 96
    	total = (total * WEIRD_PRIME + value) % arrLength
    }
    return total
}
```

#### Hash Collision.
- Separate Chaining. (When collision happens, using extra data structure, such as Array or Linkedlist)
- Linear Probing. (When collision happens, searching through table to find the next empty slot)

## HashTable - simple implementation. (using Separate Chaining)

```javascript
class HashTable {
    constructor(size = 53) {
        this.keyMap = new Array(size)
    }

    _hash(key) {
        let total = 0
        // Prime number is helpful in distributing data uniformly.
        let WEIRD_PRIME = 31

        for (let i = 0; i < Math.min(key.length, 30); i++) {
            let char = key[i]
            let value = char.charCodeAt(0) - 96
            total = (total * WEIRD_PRIME + value) % this.keyMap.length
        }
        return total
    }

    set(key, value) {
        const index = this._hash(key)

        if (!this.keyMap[index]) {
            this.keyMap[index] = []
        }

        // If encounter one existed key, usually overrides the value.
        // ...

        this.keyMap[index].push([key, value])

        return value
    }

    get(key) {
        const index = this._hash(key)

        if (this.keyMap[index]) {
            for (const [k, v] of this.keyMap[index]) {
                if (k === key) return v
            }
        }

        return undefined
    }

    keys() {
        const keysArr = []
        for (let i = 0; i < this.keyMap.length; i++) {
            if (this.keyMap[i]) {
                for (let j = 0; j < this.keyMap[i].length; j++) {
                    keysArr.push(this.keyMap[i][j][0])
                }
            }
        }

        return keysArr
    }
}
```