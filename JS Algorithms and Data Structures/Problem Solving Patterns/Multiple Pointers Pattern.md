# Multiple Pointers
Creating **pointers** or values that correspond to an index or position

and move towards the beginning, end, or middle based on a certain condition.

**Very** efficient for solving problems with minimal space complexity as well.

---

### SumZero
Write a function called sumZero which accepts a sorted array of integers.

The function should find the first pair where the sum is zero. Return an array

that includes both values that sum to zero or false if a pair does not exist.

```javascript

const arr = [-9, -3, -2, 0, 2, 3, 4, 8, 10]

function sumZero(arr) {
    let left = 0, right = arr.length - 1
    
    while (left < right) {
        if (arr[left] + arr[right] === 0) return [arr[left], arr[right]]
        
        if (arr[left] + arr[right] < 0) left++
        
        if (arr[left] + arr[right] > 0) right--
    }

    return false
}

sumZero(arr)

```


### CountUniqueValues
Implement a function called countUniqueValues, which accepts a sorted array,

and counts the unique values in the array. There can be negative numbers in

the array, but it will always be sorted.

```javascript

const arr2 = [-2, -2, 0, 0, 1, 1, 1, 2, 3, 4, 5, 5, 5, 5, 6]

function countUniqueValues(param) {
    if (param.length === 0) return 0
    
    let i = 0
    const arr = [...param]

    for (let j = 1; j < arr.length; j++) {
        if (arr[i] !== arr[j]) {
            i++
            arr[i] = arr[j]
        }
    }
    return i + 1
}

countUniqueValues(arr2)

```
