# Searching Algorithms

## Linear Search `O(n)`

Linear search is a simple search that checks every single value in order until the correct one is found, like the example below. `indexOf, includes, find, findIndex` all work with linear search.

```js
function linearSearch(arr, val) {
    for(let i = 0; i < arr.length; i++) {
        if (arr[i] === val) return i
    }
    return -1
}
```

## Binary Search `O(log n)`

Binary search only works on sorted arrays, however it is much faster because it eliminates half of the items at once.

```js
function binarySearch(arr, elem) {
    let start = 0
    let end = arr.length - 1
    let middle = Math.floor(start + end / 2)
    while(arr[middle] !== elem && start <= end) {
        if(elem < arr[middle]) {
            end = middle - 1
        } else {
            start = middle + 1
        }
        middle = Math.floor((start + end) / 2)
    }
    return arr[middle] === elem ? middle : -1
}
```
