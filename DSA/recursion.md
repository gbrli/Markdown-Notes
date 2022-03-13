# Recursion

A problem can be solved either with iteration, or recursion.

A recursion function is a function that calls itself over and over again. It should use a different input until it reaches the base case, meaning its end point.

The call stack in JS is a data structure that contains all the functions written in a program. Any time we invoke a function, it gets pushed to the top of the stack. When a function ends, the compiler will pop it off the stack. The call stack tool in the dev tools debugger will give access to the call stack and see what order functions are being executed. Recursive functions will keep pushing new functions onto the call stack, so setting an end is necessary.

## Examples

**Any recursive function must have a base case and different inputs.** Forgetting the base case will result in a stack overflow.

Come up with the function return first, then with the base case.

Counting down from the parameter to 0:

```js
function countDown(num) {
    // base case
    if (num <= 0) {
        console.log("All done")
        return
    }
    // input change and function called again
    console.log(num)
    num--
    countDown(num)
}
```

Sum of all numbers from the parameter to 1. The function is waiting in the call stack for the result of the second sumRange function, which in turn will wait until it all reaches 1. The result of `sumRange(5)` will be `5 + 4 + 3 + 2 + 1` and return `15`.

```js
function sumRange(num) {
    // base case
    if (num === 1) return 1
    // input change and recursive call
    return num + sumRange(num - 1)
}
```

Factorial functions, iterative and recurise. The recursive example returns `5 * 4 * 3 * 2 * 1`: the first functions waits in the call stack until all the individual values down to `1` are returned.

```js
// iterative factorial
function factorial(num) {
    let total = 1
    for (let i = num; i > 1; i--) {
        total *= i
    }
    return total
}

// recursive factorial
function factorial(num) {
    // base case
    if (num === 1) return 1
    // input change and recursive call
    return num * factorial (num - 1)
}
```

## Helper Method Recursion

A recursive helper function is placed inside an outer function that is iterative. They are commonly used to collect data (for example, from an array).

```js
function collectOddNum(arr) {
    let result = []
    function helper(helperInput) {
        // base case
        if(helperInput.length === 0) {
            return
        }
        if(helperInput[0] % 2 !== 0) {
            result.push(helperInput[0])
        }
        helper(helperInput.slice(1))
    }
    helper(arr)
    return result
}
collectOddNum([1,2,3,4,5,6,7,8,9,10])
```

## Pure Recursion

The same function above in pure recursion. If called with `[1,2,3,4,5]`, it will return the following

```js
[1].concat([].concat([3].concat([].concat([5].concat([])))))
```

which equals in the end to `[3, 5]`.

```js
function collectOddNum(arr) {
    // new array will be empty each time it runs
    let newArr = []
    // base case
    if (arr.length === 0) {
        return newArr
    }
    // check if first index is even and push it to array
    if(arr[0] % 2 !== 0) {
        newArr.push(arr[0])
    }
    // recursive call placed inside the first function array, waiting for the other newArr from future calls
    newArr = newArr.concat(collectOddNum(arr.slice(1)))
    return newArr
}
collectOddNum([1,2,3,4,5])
```

Tips:

* For arrays, use `slice, spread operator and concat` to make copies.
* For strings, use `slice, substr or substring` to make copies because they are immutable.
* Make copies of objects with `Object.assign or the spread operator`.

```js
function fib(n) {
    if (n <= 2) return 1
    return fib(n-1) + fib(n-2)
}
```
