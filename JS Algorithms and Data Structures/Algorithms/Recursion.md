# Recursion
A process(a function in our case) that calls itself with different input, 
and set a base case to stop the call process, or it could cause stack overflow.


### Fibonacci
```javascript
// 1. Fibonacci - recursive version. O(2^n)
function recurFibonacci(n) {
    if (n < 2) return n
    return recurFibonacci(n - 1) + recurFibonacci(n - 2)
}


// 2. Fibonacci - iterative version. O(n)
function iteraFibonacci(n) {
    const arr = [0, 1]
    for(i = 2; i < n + 1; i++) arr.push(arr[i - 2] + arr[i - 1])
    return arr[n]
}


// 3. Fibonacci - Dynamic Programming. O(n)
// Dynamic Programming is a method for solving a complex problem by breaking it down 
// into a collection of simpler subproblems, solving each of those subproblems just once, 
// and storing their solutions using a memory-based data structure
function DPFibonacci() {
    const cache = {}

    return function recurFibonacci(n) {
        if (n in cache) return cache[n]
        if (n < 2) return n

        return cache[n] = recurFibonacci(n - 1) + recurFibonacci(n - 2)
    }
}


// 4. Fibonacci - Tail Call Optimization version. O(n)
// Tail Call Optimization - make function calls without growing the call stack. (ES6, partial support)
function tcoFibonacci(n) {
    function fibAcc(n, a, b) {
        if (n === 0) return a
        return fibAcc(n - 1, b, a + b)
    }
  
    return fibAcc(n, 0, 1)
}
```

---

### Factorial - recursive version.
```javascript
function factorial(n) {
    if (n === 1) return 1
    return n * factorial(n - 1)
}
```

### Factorial - Tail Call Optimization version.
```javascript
function factorial(n) {
    function facAcc(n, acc) {
        if (n === 1) return acc
        return facAcc(n - 1, n * acc)
    }

    return facAcc(n, 1)
}
```
