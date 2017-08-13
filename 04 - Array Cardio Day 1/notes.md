## Part 4 - Array Cardio Day 1

`console.table()`, `filter()`, `map()`, `sort()`, `reduce()`

### filter

[`Array.prototype.filter()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) creates a new array with all elements that pass the test implemented by the provided function.

- Here I learned a compact way to return a value instead of an if-statement returning `true`.

```
const fifteens = inventors.filter(inventor => (inventor.year >= 1500 && inventor.year < 1600));
```

- Using `console.table()` instead of `console.log()` displays results, like a table more clearly.

### map

[`Array.prototype.map()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) creates a new array with the results of calling a provided function on every element in this array. (takes in an array, modifies it and returns a new array)

- Use `+` for concatenation in JS.

Example:

```
const fullNames = inventors.map(inventor => inventor.first + ' ' + inventor.last);
```

Another way of writing the same line of code without using `+` for concatenation:

```
const fullNames = inventors.map(inventor => `${inventor.first} ${inventor.last}`);
```

### sort

[`Array.prototype.sort()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) sorts the elements of an array *in place* and returns the array.

- The default sort order is according to string Unicode code points.

- `sort()` also accepts the specific function that defines the sort order.

Example:

```
const ordered = inventors.sort((a, b) => (a.year > b.year) ? 1 : -1);
```

In this case, we can also write it more shortly for an **ascending order** just like this:

```
const ordered = inventors.sort((a, b) => a.year - b.year);
```

### combination of filter and map

```
const de = links
           .map(link => link.textContent)
           .filter(streetName => streetName.includes('de'));
```
- **[NOTICE]**: Since `nodeList` is **NOT** an `array`, we need to turn it into an array first to manipulate array methods.

Example:

```
const links = Array.from(document.querySelectorAll('.mw-category a'));
```

Above code can rewrite into ES6 syntax like:

```
const links = [...(document.querySelectorAll('.mw-category a'))];
```

### reduce

[`Array.prototype.reduce()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) is a method that applies a function against an accumulator and each value of the array(from left-to-right) to reduce it to a single value.

Example:

```
const transportation = data.reduce(function(obj, item) {
  if(!obj[item]) {
    obj[item] = 0;
  }
  obj[item] ++;
  return obj;
}, {});
```

`obj` is an element passed in to the `reduce()` function which will gather data over each iteration. The result is just reduced the "numbers" collection into the "total" variables, which means every time you find yourself going from a list of values to one value (reducing), then you can use this method.

Example:

```
const sum = [0, 1, 2, 3, 4].reduce((a, b) => a + b, 0);

console.log(sum);  // 10
```
