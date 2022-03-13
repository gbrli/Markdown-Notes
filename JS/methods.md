# Methods

## Map

Map loops through an array and returns a new one. With replace, the first below will capitalize the first letter of each array element. The second will format the array with a paragraph tag.

```js
console.log(names.map(word => word.replace(word[0], word[0].toUpperCase())))

console.log(pokemon.map(pokemon => "<p>" + pokemon + "</p>"))

```
