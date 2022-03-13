# Sorting Algorithms

Sorting is the process of rearranging the items in a collection such as an array so that the items are in some kind of order. JS's sort() built-in method sorts items by their unicode number, but this can be changed by giving it a function where we specify a different sorting method.

## Elementary Sorting `O(n²)`

Bubble sorting and selection sorting perform very well with nearly sorted data. Insertion sorting performs very well when data is coming in live, one at a time.

All three methods are roughly equivalent in terms of performance and work best with small data sets, but they don't scale well.

### Bubble Sort

In a bubble sort, the biggest bubbles rise to the surface. Two values are being compared, and the largest one swaps to the right until it is in the right position.

```js
function bubbleSort(arr) {
    let noSwaps
    for(let i = arr.length; i > 0; i--) {
        noSwaps = true
        for(let j = 0; j < i - 1; j++) {
            if(arr[j] > arr[j+1]){
                let temp = arr[j]
                arr[j] = arr[j+1]
                arr[j+1] = temp
                noSwaps = false
            }
        }
        if(noSwaps) break
    }
    return arr
}
```

### Selection Sort

Selection sort works similar to bubble sort, but instead of large values first, it places small values in the right position first.

```js
function selectionSort(arr) {
  const swap = (arr, idx1, idx2) =>
    ([arr[idx1], arr[idx2]] = [arr[idx2], arr[idx1]]);

  for (let i = 0; i < arr.length; i++) {
    let lowest = i;
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[lowest] > arr[j]) {
        lowest = j;
      }
    }
    if (i !== lowest) swap(arr, i, lowest);
  }
  return arr;
}
```

### Insertion Sort

Insertion sort builds up the sort by gradually creating a larger left half which is always sorted. It checks a number on the right and inserts it in the right place on the left.

```js
function insertionSort(arr){
    let currentVal;
    for(let i = 1; i < arr.length; i++){
        currentVal = arr[i];
        for(let j = i - 1; j >= 0 && arr[j] > currentVal; j--) {
            arr[j+1] = arr[j]
        }
        arr[j+1] = currentVal;
    }
    return arr;
}
```

## More Efficient Sorting `O(nlog n)`

Merge sort and quick sort both use recursion and they are comparison sorts. They are faster than elementary sorts.

Radix sort does not make direct comparisons between elements.

### Merge Sort

* Split a sorted array in multiple subarrays until you have pairs
* Sort the pairs from the bottom up

```js
// merging function
function merge(arr1, arr2){
    let results = [];
    let i = 0;
    let j = 0;
    // while there is data in both arrays
    while(i < arr1.length && j < arr2.length){
      // if the second number is bigger, push the first one, else push the second one
        if(arr2[j] > arr1[i]){
            results.push(arr1[i]);
            i++;
        } else {
            results.push(arr2[j])
            j++;
        }
    }
    // while there are numbers remaining in the first array place them at the end of the new array
    while(i < arr1.length) {
        results.push(arr1[i])
        i++;
    }
    // while there are numbers remaining in the second array place them at the end of the new array
    while(j < arr2.length) {
        results.push(arr2[j])
        j++;
    }
    return results;
}
merge([100,200], [1,2,3,5,6])

// sorting function
function mergeSort(arr){
    // base case is stopping at array length of 1 or 0, meaning the left and right arrays below
    if(arr.length <= 1) return arr;
    // define middle of array
    let mid = Math.floor(arr.length/2);
    // define left half from index 0 to mid
    let left = mergeSort(arr.slice(0,mid));
    //define right side from mid to end
    let right = mergeSort(arr.slice(mid));
    // the left and right sides become recursive parameters
    // return the two array halves merged with the merge function
    return merge(left, right);
}
mergeSort([10,24,76,73])
```

### Quick Sort

Quick sort uses a pivot helper to match values and swaps in order to sort.

```js
function pivot(arr, start = 0, end = arr.length - 1) {
  const swap = (arr, idx1, idx2) => {
    [arr[idx1], arr[idx2]] = [arr[idx2], arr[idx1]];
  };

  // We are assuming the pivot is always the first element
  let pivot = arr[start];
  let swapIdx = start;

  for (let i = start + 1; i <= end; i++) {
    if (pivot > arr[i]) {
      swapIdx++;
      swap(arr, swapIdx, i);
    }
  }

  // Swap the pivot from the start the swapPoint
  swap(arr, start, swapIdx);
  return swapIdx;
}

function quickSort(arr, left = 0, right = arr.length -1){
    if(left < right){
        let pivotIndex = pivot(arr, left, right) //3
        //left
        quickSort(arr,left,pivotIndex-1);
        //right
        quickSort(arr,pivotIndex+1,right);
      }
     return arr;
}      
quickSort([100,-3,2,4,6,9,1,2,5,3,23])
```

### Radix Sort

It creates 10 buckets for each number. According to the decimal place in a number, it places them in the bucket, reorganizes the data, then divides in the buckets again by the next decimal place.

```js
function getDigit(num, i) {
  return Math.floor(Math.abs(num) / Math.pow(10, i)) % 10;
}

function digitCount(num) {
  if (num === 0) return 1;
  return Math.floor(Math.log10(Math.abs(num))) + 1;
}

function mostDigits(nums) {
  let maxDigits = 0;
  for (let i = 0; i < nums.length; i++) {
    maxDigits = Math.max(maxDigits, digitCount(nums[i]));
  }
  return maxDigits;
}

function radixSort(nums){
    let maxDigitCount = mostDigits(nums);
    for(let k = 0; k < maxDigitCount; k++){
        let digitBuckets = Array.from({length: 10}, () => []);
        for(let i = 0; i < nums.length; i++){
            let digit = getDigit(nums[i],k);
            digitBuckets[digit].push(nums[i]);
        }
        nums = [].concat(...digitBuckets);
    }
    return nums;
}
radixSort([23,345,5467,12,2345,9852])
```
