# Insertion Sort
Builds up the sort by gradually creating a larger left half which is always sorted.

### Big O
- time complexity
  - best case -> **O(n)**
  - average case -> **O(n^2)**
  - worst case -> **O(n^2)**
- space complexity
  - worst case -> **O(1)**

```javascript

var arr = [2, 99, 8, 5, 77, 33, 6, 0, 99, 38, 7, 52, -7]

function insertionSort(data) {
    const arr = [...data]

    for (let i = 1; i < arr.length; i++) {
        let j = i - 1, curVal = arr[i]

        for (; j >= 0 && curVal < arr[j]; j--) {
            arr[j + 1] = arr[j]
        }
        arr[j + 1] = curVal
    }
    
    return arr
}

insertionSort(arr)

```