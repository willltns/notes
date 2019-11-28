# Merge Sort

##### Divide and Conquer.

- Combination of two things - merge & sort.
- Arrays of 0 or 1 element are always sorted.
- Works by decomposing an array into smaller arrays of 0 or 1 element, then merging and building up a newly sorted array.

```javascript
function merge(arr1, arr2) {
    let lIndex = 0, rIndex = 0, arr = []

    while (lIndex < arr1.length && rIndex < arr2.length) {
        if (arr1[lIndex] < arr2[rIndex]) {
            arr.push(arr1[lIndex])
            lIndex++
        } else {
            arr.push(arr2[rIndex])
            rIndex++
        }
    }

    while (lIndex < arr1.length) {
        arr.push(arr1[lIndex])
        lIndex++
    }
    while (rIndex < arr2.length) {
        arr.push(arr2[rIndex])
        rIndex++
    }

    return arr
}

function mergeSort(arr) {
    if (arr.length <= 1) return arr
    
    const middle = Math.floor(arr.length / 2)

    const right = arr.slice(0, middle)
    const left = arr.slice(middle)

    const arr1 = mergeSort(right)
    const arr2 = mergeSort(left)

    return merge(arr1, arr2)
}
```