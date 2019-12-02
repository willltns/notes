# Quick Sort

- Arrays of 0 or 1 element are always sorted.
- Works by selecting one element(called the `pivot`) and finding the index where the pivot should end up in the sorted array.
- Once the pivot is positioned appropriately, quick sort can be applied on either side of the pivot.

### Big O
- time complexity
  - best case -> **O(n\*log(n))**
  - average case -> **O(n\*log(n))**
  - worst case -> **O(n^2)**
- space complexity
  - worst case -> **O(log(n))**

```javascript
var arr = [33, 6, 88, 5, 11, 26, 77, 37, 50, 21]

function pivot(arr, start, end) {
    let pivotIndex = start
    const pivotValue = arr[start]

    for (let i = pivotIndex + 1; i <= end; i++) {
        if (arr[i] < pivotValue) {
            pivotIndex++

            if (pivotIndex !== i) {
                // SWAP (ES6)
                [ arr[pivotIndex], arr[i] ] = [ arr[i], arr[pivotIndex] ]
            }
        }
    }

    arr[start] = arr[pivotIndex]
    arr[pivotIndex] = pivotValue

    return pivotIndex
}

function quickSort(arr, start, end) {
    if (start >= end) return arr

    const pivotIndex = pivot(arr, start, end)

    quickSort(arr, start, pivotIndex - 1)
    quickSort(arr, pivotIndex + 1, end)

    return arr
}


quickSort(arr, 0, arr.length - 1)

```