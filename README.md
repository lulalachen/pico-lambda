<h1 align="center">pico-lambda</h1>

<div align="center">
  λ
</div>
<div align="center">
  <strong>Arrays the functional way</strong>
</div>
<div align="center">
  A <code>460b</code> functional library based on native array methods
</div>

<div align="center">
  <!-- Stability -->
  <a href="https://nodejs.org/api/documentation.html#documentation_stability_index">
    <img src="https://img.shields.io/badge/stability-experimental-orange.svg?style=flat-square"
      alt="API stability" />
  </a>
  <!-- Downloads -->
  <a href="https://npmjs.org/package/pico-lambda">
    <img src="https://img.shields.io/npm/dm/pico-lambda.svg?style=flat-square"
      alt="Downloads" />
  </a>
  <!-- Semi Standard -->
  <a href="https://github.com/Flet/semistandard">
    <img src="https://img.shields.io/badge/code%20style-semistandard-brightgreen.svg?style=flat-square"
      alt="semistandard" />
  </a>
</div>

## why pico-lambda
- **Pico:** weighs less than 460 bytes gzipped.
- **Useful:** takes most native JavaScript array methods and makes them immutable, curried, and composable.
- **Familiar:** same names just curried and composable [JavaScript Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)..

> Pico-lambda was made for the ES2015 Javascript Runtime. It has no dependencies.

* * *

## Example

After installing via `npm install`:

```js
const {
  concat,
  filter,
  map,
  reduce,
  compose
} = require('pico-lambda')

//concat
const arrayOne = [1, 2, 3];
const addTwo = concat([4, 5])
const result = addTwo(arrayOne)

// We can compose instead of chaining
compose(
  reduce((acc, val) => val + acc, 0),
  map(x => x * 2),
  filter(x => x > 5),
  concat([6, 7, 8])
)([1, 2, 3, 4, 5])
```

* * *

## Api
### compose :: `((e -> f), ..., (b -> c), (a -> b)) -> a -> f`
Evaluates the provided functions, right to left, passing the return value
of each function to the next in line.
The initial function is passed the initial value provided to comopse.
The output of the final function, in this case `(e->f)`, is returned.
### concat :: `[a] -> ([a], ..., [a]) -> [a]`
Concatenates two arrays
```js
concat([4, 5])([1,2,3])    // => [1, 2, 3, 4, 5]
concat([4, 5])([1,2], [3]) // => [1, 2, 3, 4, 5]
```
> See [Array.concat (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat)

### copyWithin :: `(Int, Int, Int) -> [a] -> [a]`
Makes a shallow copy of part of an array and overwrites another location in the same with the copy. Size is kept constant.

> See [Array.copyWithin (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/copyWithin)

### entries:: `[a] -> [b]`
Return an iterator over key, value pairs from the array.

> See [Array.entries (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/entries)

### every  :: `((a, Int, [a]) -> Boolean) -> [a] -> Boolean`
Applies predicate to all elements in array and returns false if any fail. The predicate function must at least take one parameter for each element but may optionally take an index and the entire array as 2nd and 3rd parameters, respectively.

> See [Array.every (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every)

### fill :: `(a, Int, Int) -> [a] -> [a]`
Fills a portion of the given array putting the same new value into each slot.

> See [Array.fill (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/fill)

### filter :: `((a, Int, [a]) -> Boolean) -> [a] -> [a]`
Returns a new array containing only those elements of the given array that pass the given predicate.

> See [Array.filter (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

### find :: `(a -> Boolean) -> [a] -> a | undefined`
Finds and returns the first element in the given array that matches the given predicate. If no element passes, undefined is returned.

> See [Array.find (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)

### findIndex :: `(a -> Boolean) -> [a] -> Int`
Returns the index of the first element in the given array that matches the given predicate. If no element passes, -1 is returned.

> See [Array.findIndex (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)

### includes :: `a -> [a] -> Boolean`
Returns true if the given element is in the given array, otherwise false.

> See [Array.includes (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)

### indexOf :: `(a, Int) -> [a] -> Int`
Returns the index of the given element if it is in the given array, otherwise -1.
The 2nd parameter can be used to change where it starts looking.

> See [Array.indexOf (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)

### join :: `String -> [a] -> String`
Converts each element of the array to a string and concatenates them together with the given string as a delimiter.

> See [Array.join (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join)

### keys :: `[a] -> [Int]`
Return an iterator over keys from the array.

> See [Array.keys (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/keys)

### lastIndexOf :: `(a, Int) -> [a] -> Int`
Works like indexOf but starts at the end and works backwards.
The 2nd parameter can be used to tell it where to start working backwards from.

> See [Array.lastIndexOf (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/lastIndexOf)

### map :: `(a -> b) -> [a] -> [b]`
Applies a function over each element in the given array, returning a new array with each functions results.

> See [Array.map (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

### pipe :: `((a -> b), (b -> c), ..., (e -> f)) -> a -> f`
Takes an initial value that is passed to the first function in the parameter list.
The return value of each subsequent function is passed to the following function.
The return value of the last function is returned from pipe.

> See [Array.pipe (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/pipe)

### pop :: `[a] -> [a]`
Returns a new array without the last item

> See [Array.pop (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)

### push :: `a -> [a] -> [a]`
Returns a new array with the new element appended to the end of the original array.

> See [Array.push (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push)

### reduce :: `((a, b) -> a) -> a -> [b] -> a`
Applies a function against an accumulator and each value of the array (from left-to-right), then returning the accumulator.

> See [Array.reduce (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)

### reduceRight :: `((a, b) -> a) -> a -> [b] -> a`
Applies a function against an accumulator and each value of the array (from right-to-left), then returning the accumulator.

> See [Array.reduceRight (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduceRight)

### reverse ::  `[a] -> [a]`
Returns a new array with the elements in reverse order.

> See [Array.reverse (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse)

### shift :: `[a] -> [a]`
Returns a new array with the first element removed.

> See [Array.shift (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/shift)

### slice :: `(int, int) -> [a] -> [a]`
Takes a slice from a given array and returns it as a new array.

> See [Array.slice (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)

### splice :: `(int, int, [a]) -> [a] -> [a]`
Returns a new array with the indicated elements removed. An optional set of new elements can be inserted in their place.

> See [Array.splice (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

### some :: `(a -> Boolean) -> [a] -> Boolean`
Returns true if any element in the given array matches the given predicate.

> See [Array.some (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some)

### sort :: `((a, a) -> int) -> [a] -> [a]`
Returns a copy of the original array with the values sorted. If a comparator function is provided it should return -1, 0 or 1 depending on whether the first element is less than, equal to or greater than the second, respectively. If no comparator is given, lexical sorting is used.

> See [Array.sort (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

### toLocaleString :: `(String, Obj) -> [a] -> String`
Converts each element of an array into a string based on current locale settings or locale options passed in. The resulting strings are appended together using commas.

> See [Array.toLocaleString (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/toLocaleString)

### toString :: `[a] -> String`
Converts each element of an array into a string and appends them together with a comma.

> See [Array.toString (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/toString)

### unshift :: `[a] -> [a]`
Returns a new copy of an array with the first element removed.

> See [Array.unshift (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift)


## Where are ...?
- `length` - This is a property, not a method, so it doesn't really belong here.
- `forEach` - This is inherently side-effect-y, it adds nothing that can't be done with `filter`, `map` and `reduce`.

If you don't agree with anything above that's great! Just log an issue so we can discuss.