# Big-O Notation

Big-O notation provides a numeric representation of the performance of any code. It allows us to measure how the runtime of an algorithm works as the inputs grow. What matters is not the details, but the general trend.

An algorithm is `O(f(n))` if the number of simple operations that the computer must run is less that a constant times `f(n)`, as `n` increases. Some examples:

* f(n) can be linear `(f(n) = n)`
* f(n) can be quadratic `(f(n) = n²)`
* f(n) can be constant `(f(n) = 1)`

Big-O notation is used to measure space and time complexity.

* Time complexity is the analysis of the runtime of an algorithm as its size of inputs increases.
* Space complexity is the analysis of how much memory needs to be allocated to run a certain algorithm.

Fastest to slowest patterns in complexity:

* O(1)
* O(log n)
* O(n)
* O(nlog n)
* O(n²)

## Calculating how long something takes to run

`performance.now()` will give the milliseconds passed since a program was started. The below returns how long one function took to run.

```js
const time = performance.now()
functionYouNeedToTime()
const time2 = performance.now()
console.log("Time elapsed: ${(time - time2) / 1000} seconds.")
```

However, this measures time in the form of milliseconds, and it is variable according to each machine, and not very exact. The best way to measure performance is by measuring the amount of operations a computer needs to perform. As in, the actual number of operators within the body of a function.

## Constant runtime

This function always runs three operations even as its input grows, so its runtime is constant: `O(1)`.

```js
function addUpTo(n) {
    return n * (n + 1) / 2
}
```

In this function, the minimum number might be `n`, but the maximum is set to a number, so ther untime is still shortened to `0(1)`.

```js
function logAtMost10(n) {
    for (let i = 1; i <= Math.min(n, 10); i++) {
        console.log(i);
    }
}
```

## Linear runtime

The operations run in this functions are proportionate to the input given to it, so the runtime is linear: `O(n)`. If the function had multiple loops in it, it would still be simplified to linear runtime, because we're only looking at the big picture of the problem.

```js
function addUpTo(n) {
    let total = 0;
    for (let i = 0; i <=n; i++) {
        total += i;
    }
    return total;
}
```

## Squared runtime

A function with a nested loop will instead feature squared runtime. The below will print pairs of numbers (00 01 02, 10 11 12, 20 21 22), so the second loop will create more operations for each operation in the first loop. So the actual runtime is `O(n * n)`, meaning `O(n²)`.

```js
function printPairs(n) {
    for (let i = 0; i <=n; i++) {
        for (let j = 0; j <=n; j++) {
            console.log(i, j);
        }
    }
}
```

## Simplyfing Notation

Constants and smaller terms don't matter as much as the big trends, so the notation is always simplified.

* O(2n) becomes `O(n)`
* O(500) becomes `O(1)`
* O(13n²) becomes `0(n²)`
* O(n + 10) becomes `O(n)`
* O(1000n + 50) becomes `O(n)`
* O(n² + 5n + 8) becomes `O(n²)`

Time complexity shorthands:

* Arithmetic operations and variable assignment are constant
* Accessing array elements by index or object elements by key is constant
* In a loop, the complexity is **the length of the loop multiplied by whatever happens inside the loop**

Space complexity shorthands in JS:

* Most primitive values (booleans, numbers, undefined and null) are constant space O(1)
* Strings require O(n), where n is the string length
* Reference types are O(n), where n is the array length of keys in an object.

## Logarithms

A logarithm is the inverse of an exponent. A binary logarithm roughly measures the number of times you can divide a number by 2 before you get a value that is <= to one. The most common type of logarithm is binary like the example below, but there are more.

`log₂(8) = 3` is the opposite of `2³ = 8`.

`8 / 2 = 4` then `4 / 2 = 2` then `2 / 2 = 1`

The division occurs 3 times, so the result is `3`.

## Objects and built-in methods

Objects have a big-O of `O(1)` for insertion, removal, and access, and `O(n)` for searching. The constant runtime makes them excellent unless you need them items in a certain order. Object methods are `O(n)` for .keys, .values and .entries, and `O(1)` for .hasOwnProperty.

## Arrays and built-in methods

Arrays are best used if you need ordered data, otherwise they can be slow. Access and insertion/removal at the end with push/pop is `O(1)`, search and insertion/removal with shift/unshift is `O(n)`.

* push/pop `O(1)`
* shift/unshift `O(n)`
* concat, slice, splice `O(n)`
* sort `O(n * log n)`
* map/filter/reduce, forEach `O(n)`
