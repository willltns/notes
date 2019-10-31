# Selection Sort
Similar to bubble sort, but instead of first placing large values into sorted position, it places small values into sorted position.

### Big O
- time complexity
  - best case -> **O(n^2)**
  - average case -> **O(n^2)**
  - worst case -> **O(n^2)**
- space complexity
  - worst case -> **O(1)**

```javascript

var arr = [2, 99, 8, 5, 77, 33, 6, 0, 99, 38, 7, 52, -7]

function selectionSort(data) {
    const arr = [...data]

    for (let i = 0; i < arr.length - 1; i++) {
        let min = i
        for (let j = i + 1; j < arr.length; j++) if (arr[min] > arr[j]) min = j
        
        if (min !== i) {
            let temp = arr[i]
            arr[i] = arr[min]
            arr[min] = temp
        }
    }

    return arr
}

selectionSort(arr)

```