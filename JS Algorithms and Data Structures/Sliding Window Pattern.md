# Sliding Window Pattern

This pattern involves creating a window which can either be an array or number from one position to another.

Depending on a certain condition, the window either increases or closes(and a new window is created).

Very useful for keeping track of a subset of data in an array/string etc.

```javascript

// Write a function called `maxSubarraySum`, which accepts an array of integers
// and a number called n, The function should calculate the maximum sum of
// n consecutive elements in the array.

var arr = [1,2,4,5,7,9,2,5,8,9,4]

function maxSubarraySum(arr, n) {
    if (n > arr.length || n < 1) return null

    let maxSum = 0, tempSum = 0

    for (let i = 0; i < n; i++) {
        maxSum += arr[i]
    }
    tempSum = maxSum

    for (let j = n; j < arr.length; j++) {
        tempSum = tempSum - arr[j - n] + arr[j]
        maxSum = Math.max(maxSum, tempSum)
    }

    return maxSum
}

maxSubarraySum(arr, 3)

```

```javascript

// Get the length of the longest substring without repeating characters.

function getLongestUniqueSubStringlength(str) {
    let curLength = 1
    let maxLength = 1
    const visitedTable = {}

    // Mark first character as visited by storing the index of first character in visitedTable.
    visitedTable[str.charAt(0)] = 0

    // Then start from the second character.
    for (let i = 1; i < str.length; i++) {
        const curChar = str.charAt(i)
        const prevIndex = visitedTable[curChar]
        
        // If the current character is not present in the already processed substring,
        // or it is not part of the current non-repeating character substring, then do curLength++
        if ((!prevIndex && prevIndex !== 0) || i - curLength > prevIndex) {
            curLength++
        } else {
            maxLength = Math.max(curLength, maxLength)
            curLength = i - prevIndex
        }

        // Update the index of current character.
        visitedTable[curChar] = i
    }
    // Last compare.
    maxLength = Math.max(curLength, maxLength)

    return maxLength
}

getLongestUniqueSubStringlength('abcdavvcfbbc')

```