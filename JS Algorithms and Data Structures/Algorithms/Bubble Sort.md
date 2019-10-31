# Bubble Sort
A sorting algorithm where the largest values bubble to the top, one at a time.

### Big O
- time complexity
  - best case -> **O(n)**
  - average case -> **O(n^2)**
  - worst case -> **O(n^2)**
- space complexity
  - worst case -> **O(1)**

```javascript

var arr = [2, 99, 8, 5, 77, 33, 6, 0, 99, 38, 7, 52, -7]

function bubbleSort(data) {
    const arr = [...data]

    let isSorted = true
    for (let i = 0; i < arr.length - 1; i++) {
        for (let j = 0; j < arr.length - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                isSorted = false

                const temp = arr[j]
                arr[j] = arr[j + 1]
                arr[j + 1] = temp
            }
        }

        if (isSorted) break
        isSorted = true
    }
    
    return arr
}

bubbleSort(arr)

```