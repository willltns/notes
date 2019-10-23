# Frequency Counter

This pattern uses objects or sets to collect values/frequencies of values.

This can often avoid the need for nested loops or O(N^2) operations with arrays/strings.

```javascript

// Write a function called same, which accepts two arrays.
// The function should return true if every value in the array 
// has it's corresponding value squared in the second array.
// The frequency of values must be the same.

const arr1 = [1, 3, 3, 6, 10]
const arr2 = [1, 9, 9, 36, 100]

function same(arr1, arr2) {
    if (arr1.length !== arr2.length) return false

    const counter1 = {}
    const counter2 = {}

    arr1.forEach(value => counter1[value] = (counter1[value] || 0) + 1)
    arr2.forEach(value => counter2[value] = (counter2[value] || 0) + 1)

    for (const key in counter1 ) {
        if (counter1[key] !== counter2[key ** 2]) return false
    }

    return true
}

console.log(same(arr1, arr2))

```

### Anagram

Given two strings, write a function to determine if the second stringis an anagram of the first.

An anagram is a word, phrase, or name formed by rearranging the letters of another, such as cinema, formed from iceman.

```javascript

function validAnagram(str1, str2) {
    if (str1.length !== str2.length) return false

    const lookup = {}

    for (i = 0; i < str1.length; i++) {
        const char = str1[i]
        lookup[char] = (lookup[char] || 0) + 1
    }

    for (i = 0; i < str2.length; i++) {
        const char = str2[i]
        
		// Cannot find letter or letter counter is zero, then it is not an anagram.
        if (!lookup[char]) return false
        else lookup[char] -= 1
    }

    return true
}

console.log(validAnagram('', '')) // true
console.log(validAnagram('qwerty', 'qertwy')) // true
console.log(validAnagram('sometime', 'sometimes')) // false
console.log(validAnagram('someday', 'sommday')) // false

```