## Part 18 - Adding Up Times with Reduce

### Grabbing times

Remember to turn the nodeList into an array:

```
const timeNodes = Array.from(document.querySelectorAll('[data-time]'));
```

### Calculating Times

Get the `dataset.time`

```
const seconds = timeNodes
  .map(timeNode => timeNode.dataset.time)

console.log(seconds);
```

`dataset.time` will be value of `data-time` attributes we set on html

Then we turn the values to the seconds unit, and use `parseFloat` to turn it to an actual number of array

```
const seconds = timeNodes
  .map(timeNode => timeNode.dataset.time)
  .map(timeCode => {
    const [mins, secs] = timeCode.split(':').map(parseFloat);
    return (mins * 60) + secs;
  })

console.log(seconds);
```

The [`parseFloat`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseFloat) function parses a string argument and returns a floating point number.

Let's `reduce` the array to get the total seconds:

```
const seconds = timeNodes
  .map(timeNode => timeNode.dataset.time)
  .map(timeCode => {
    const [mins, secs] = timeCode.split(':').map(parseFloat);
    return (mins * 60) + secs;
  })
  .reduce((total, vidSeconds) => total + vidSeconds);    // total seconds 17938

console.log(seconds);
```

### Figure out the total time

Use the `seconds` (total seconds) variable to calculate the `hours` and `mins`, use `Math.floor` to remove decimal point

```
let secondsLeft = seconds;
const hours = Math.floor(secondsLeft / 3600);
secondsLeft = secondsLeft % 3600;

const mins = Math.floor(secondsLeft / 60);
secondsLeft = secondsLeft % 60;
```
