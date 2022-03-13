# JS Challenges

## Pangram check

```js
const abc = 'abcdefghijklmnopqrstuvwxyz'

const isPangram = (string) => {
    // const processedString = [...new Set(string.toLowerCase().split(' ').join(''))].sort().join('')
    const regexMatch = new Set(string.toLowerCase().match(/[a-z]/gi))
    return regexMatch.size===26
}
```

## Using array methods on API results

```js
const getUsers = async () => {
    const api = 'https://jsonplaceholder.typicode.com/users'
    const response = await fetch(api)
    const json = await response.json()
    
    const result = json.filter(v=>v.name.toLowerCase().includes('k')).map(({name,email})=>({name,email}))
    
    return result
}

(async function() {
    try{
     console.log(await getUsers())   
        
    }catch(err){
        console.log(err)
    }
})();
```

## Fizzbuzz but with numbers

```js
const toRainLanguage = (number)=>{
    let result = ''
    if(number%3===0) result += "Pling"
    if(number%5===0) result += "Plang"
    if(number%7===0) result += "Plong"
    
    return result || number
}
```

## Isogram check

```js
const isIsogram = (string) => {
    
    const lowerCased = string.toLowerCase() 
    const result = lowerCased.split('').every((v,i)=>console.log(v,i) || lowerCased.indexOf(v)===i)
    
    return result

}
console.log(isIsogram('ambidExtRously')) // true
console.log(isIsogram('patteRN')) // false
```

## Leap Year check

```js
const isLeapYear = (numberYear) => {
    const numberYear = Number(year)
    return numberYear % 100 === 0 ? numberYear % 400 === 0 : numberYear % 4 === 0
}
```

## Runlength encode/decode

```js
const encode = (string)=>{
    return string.replace(/(\w)\1+/g, (m,v) => `${m.length}${v}`)
}

const decode = (string)=>{
    return string.replace(/(\d+)(\w)/g, (x,y,z) => z.repeat(y))
}
```

## Reduce() examples

```js
// remove duplicates
const removeDuplicateValues = (array) => {
   return array.reduce((accumulator,value)=>{
       return accumulator.includes(value) ? accumulator : [...accumulator, value]
   },[])
}

console.log(
  removeDuplicateValues(["one", "two", "one", "three", "three", "two"])
); // ['one','two','three']
```

```js
/// map() recreated with reduce()
const map = (array, callback) => {
   return array.reduce((accumulator,value)=>{
     return [...accumulator, callback(value)]
   },[])
}

console.log(map([1, 2, 3], (v) => v * v));
```

## Anagram check using frequency counter pattern

```js
function validAnagram(first, second) {
    if (first.length !== second.length){
     return false
    }
    const lookup = {}

    for (let i = 0; i < first.length ; i++) {
        let letter = first[i]
        lookup[letter] ? lookup[letter] += 1 : lookup[letter] = 1
    }

    for (let i = 0; i < second.length ; i++) {
        let letter = second[i]
        if (!lookup[letter]) {
            return false
        } else {
            lookup[letter -= 1]
        }
    }
    return true
}
```

## Count unique values using multiple pointers pattern

```js
function count(arr) {
    if (arr.length === 0) {
        return 0
    }
    let i = 0
    for (let j = 1; j < arr.length; j++){
        if (arr[i] !== arr[j]) {
            i++
            arr.[i] = arr[j]
        }
    }
    return i + 1
}
```

## Check max sum of a subarray with sliding window pattern

```js
function maxSubarraySum(arr, num) {
    lex max = 0
    let temp = 0
    if (arr.length < num) return null
    for (let i = 0; i < num; i++) {
        max += arr[i]
    }
    temp = max
    for (let i = num; i < arr.length; i++) {
        temp = temp - arr[i - num] + arr[i]
        max = Math.max(max, temp)
    }
    return max
}
```

## Search with divide and conquer pattern - binary search

```js
function search(array, val) {
    let min = 0
    let max = array.length - 1

    while (min <= max) {
        let middle = Math.floor((min + max) / 2)
        let currentElement = array[middle]

        if (array[middle] < val) {
            min = middle + 1
        } else if (array[middle] > val) {
            max = middle - 1
        } else {
            return middle
        }
    }
    return -1
}
```

## FCC Intermediate Challenges

### Sum All Numbers in a Range

```js
function sumAll(arr) {
  // find smallest and biggest between two numbers
  let max = Math.max(arr[0], arr[1]);
  let min = Math.min(arr[0], arr[1]);
  let sumBetween = 0;
  // loop from the smallest to the biggest and add to sum
  for (let i = min; i <= max; i++) {
    sumBetween += i;
  }
  return sumBetween;
}

sumAll([1, 4]);
```

### Return unique elements from two arrays

```js
function diffArray(arr1, arr2) {
  // merge the two arrays, filter will return an array of the unique items
  // includes will check for the item that is being filtered, return true or false and 
  return arr1
    .concat(arr2)
    .filter(item => !arr1.includes(item) || !arr2.includes(item));
}

diffArray([1, 2, 3, 5], [1, 2, 3, 4, 5]);
```

### Remove values present in an array

```js
// the values to remove are passed to the rest operator, which takes multiple function parameters
function destroyer(arr, ...valsToRemove) {
  // returning what is not included in the valsToRemove
  return arr.filter(elem => !valsToRemove.includes(elem));
}
destroyer([1, 2, 3, 1, 2, 3], 2, 3);
```

### Check an array of objects for whatever matches the second parameter, also an object

```js
function whatIsInAName(collection, source) {
  // find key name of the source
  var srcKeys = Object.keys(source);
  // filter the collection by looping through each item in the object
  // check if the obj has the property in source
  return collection.filter(function(obj) {
    for (var i = 0; i < srcKeys.length; i++) {
      if (
        !obj.hasOwnProperty(srcKeys[i]) ||
        obj[srcKeys[i]] !== source[srcKeys[i]]
      ) {
        return false;
      }
    }
    return true;
  });
}

whatIsInAName(
  [
    { first: "Romeo", last: "Montague" },
    { first: "Mercutio", last: null },
    { first: "Tybalt", last: "Capulet" }
  ],
  { last: "Capulet" }
);
```

### Convert to spinal case (all-lowercase-joined-by-dashes)

```js
function spinalCase(str) {
  // split the string whenever it encounters a space \s, an underscore _, or where it is followed by an uppercase letter (?=[A-Z])
  return str
    .split(/\s|_|(?=[A-Z])/)
    .join("-")
    .toLowerCase();
}
```

### Pig Latin

```js
function translatePigLatin(str) {
  // get a match of consonants (not vowels). will be null if it starts with vowels
  let consonantRegex = /^[^aeiou]+/;
  let myConsonants = str.match(consonantRegex);
  // if the word starts with a consonant, it replaces it with an empty space, then concats the rest of the string and ay at the end
  return myConsonants !== null
    ? str
        .replace(consonantRegex, "")
        .concat(myConsonants)
        .concat("ay")
    : str.concat("way");
}
translatePigLatin("consonant");
```

### Replace word but keep same case

```js
function myReplace(str, before, after) {
  // check if first character of argument "before" is a capital or lowercase letter and change the first character of argument "after" to match the case
  if (/^[A-Z]/.test(before)) {
    after = after[0].toUpperCase() + after.substring(1)
  } else {
    after = after[0].toLowerCase() + after.substring(1)
  }
  return str.replace(before, after);
}
myReplace("A quick brown fox jumped over the lazy dog", "jumped", "leaped");
```

### Find the missing letter in a range

```js
function fearNotLetter(str) {
  // loop over the entire string and find the unicode char code at the specified index. if the difference between one and the one before it is not 1, meaning they are not in a sequence, it will return the missing one
  for (let i = 1; i < str.length; ++i) {
    if (str.charCodeAt(i) - str.charCodeAt(i - 1) > 1) {
      return String.fromCharCode(str.charCodeAt(i - 1) + 1);
    }
  }
}
```

### Create an array of multiple arrays without duplicates

```js
function uniteUnique(...arrays) {
  //make an array out of the given arrays and flatten it (using the spread operator)
  const flatArray = [].concat(...arrays);
  // create a Set which clears any duplicates since it's a regular set and not a multiset
  return [...new Set(flatArray)];
}
uniteUnique([1, 3, 2], [5, 2, 1, 4], [2, 1]);
```

### Convert to HTML characters

```js
function convertHTML(str) {
  // declare entities as objects
  const htmlEntities = {
    "&": "&amp;",
    "<": "&lt;",
    ">": "&gt;",
    '"': "&quot;",
    "'": "&apos;"
  };
  // replace entities with match
  return str.replace(/([&<>\"'])/g, match => htmlEntities[match]);
}
convertHTML("Dolce & Gabbana");
```

### Return sum of odd fib numbers

```js
function sumFibs(num) {
  let prevNumber = 0;
  let currNumber = 1;
  let result = 0;
  while (currNumber <= num) {
    if (currNumber % 2 !== 0) {
      result += currNumber;
    }
    currNumber += prevNumber;
    prevNumber = currNumber - prevNumber;
  }
  return result;
}
sumFibs(4);
```

### Return sum of all prime numbers

```js
function sumPrimes(num) {
  // Helper function to check primality
  function isPrime(num) {
    for (let i = 2; i <= Math.sqrt(num); i++) {
      if (num % i == 0)
        return false;
    }
    return true;
  }
  // Check all numbers for primality
  let sum = 0;
  for (let i = 2; i <= num; i++) {
    if (isPrime(i))
      sum += i;
  }
  return sum;
}
```

## Find smallest common multiple

```js
function smallestCommons(arr) {
  // Setup
  const [min, max] = arr.sort((a, b) => a - b);
  const range = Array(max - min + 1)
    .fill(0)
    .map((_, i) => i + min);
  // Largest possible value for SCM
  const upperBound = range.reduce((prod, curr) => prod * curr);
  // Test all multiples of 'max'
  for (let multiple = max; multiple <= upperBound; multiple += max) {
    // Check if every value in range divides 'multiple'
    const divisible = range.every((value) => multiple % value === 0);
    if (divisible) {
      return multiple;
    }
  }
}
smallestCommons([1, 5]);
```

### Flatten nested arrays

```js
function steamrollArray(arr) {
  const flat = [].concat(...arr);
  return flat.some(Array.isArray) ? steamrollArray(flat) : flat;
}
steamrollArray([1, [2], [3, [[4]]]]);
```

### Binary to decimal converter

```js
function binaryAgent(str) {
  return String.fromCharCode(
    ...str.split(" ").map(function(char) {
      return parseInt(char, 2);
    })
  );
}

binaryAgent(
  "01000001 01110010 01100101 01101110 00100111 01110100 00100000 01100010 01101111 01101110 01100110 01101001 01110010 01100101 01110011 00100000 01100110 01110101 01101110 00100001 00111111"
);
```

### Check that objects are all truthy

```js
function truthCheck(collection, pre) {
  return collection.every(obj => obj[pre]);
}

truthCheck(
  [
    { user: "Tinky-Winky", sex: "male" },
    { user: "Dipsy", sex: "male" },
    { user: "Laa-Laa", sex: "female" },
    { user: "Po", sex: "female" }
  ],
  "sex"
);
```
