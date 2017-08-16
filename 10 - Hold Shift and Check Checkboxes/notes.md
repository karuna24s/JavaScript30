## Part 10 - Hold Shift and Check checkboxes

### Fetch all the `<input>` elements and `addEventListener`

```
const checkboxes = document.querySelectorAll('.inbox input[type="checkbox"]');
checkboxes.forEach(checkbox => checkbox.addEventListener( 'click', handleCheck ));  // `click` also fires when we use the keyboard
```

### Checking steps

- Steps:
  1. Check an input a <- will be the `lastChecked`
  2. Hold shift key
  3. Check an input b <- will be `this`
  4. Then we want to confirm that all the inputs between a and b will also be checked <- `inBetween`'s inputs `.checked = true`;


```
let lastChecked;

function handleCheck(e) {
  // console.log(e);
  // check if they have shift key down
  // and check that they are checking it
  let inBetween = false;
  if(e.shiftKey && this.checked) {
    // go ahead and do what we please
    // loop over every single checkbox
    checkboxes.forEach(checkbox => {
      console.log(checkbox);
      if(checkbox === this || checkbox === lastChecked) {
        inBetween = !inBetween;
        console.log('Starting to check them inbetween');
      }

      if(inBetween) {
        checkbox.checked = true;
      }
    });
  }

  lastChecked = this;
}
```

 - We defined the range of `inBetween` by `checkbox === this` and `checkbox === lastChecked`

 - We check all the inputs, if it's one of the two inputs we checked, then flip the `inBetween = true`, and set all the `inBetween = true` inputs ' `.checked = true`

### Where I was confused:

Let's take a look at some pseudo-code:

```
let inBetween = false;
// First selected b, then hold shiftKey and selected d
//start checking
[ ] a  <- inBetween = false, it doesn't get in the if condition
[X] b  <- inBetween = true, b is the checked input 'lastChecked', and inBetween starts to flip to true
[X] c  <- inBetween = true
[X] d  <- inBetween = false, d is the checked input 'this', and its inBetween is fliped from true to false, then the checking ended as well.
[ ] e  <- inBetween = x, it doesn't get in the if condition
```

I've got stuck in a long time for that iterating to the input c, how come `inBetween` is true, seems like it doesn't match either `checkbox === this` or `checkbox === lastChecked`, is it because the `inBetween` had flipped to true so that it's true when checking on input c, right ?

### Let's face to some problems

- Problem 1: If you reload the page and hold shift key directly, then select one input, the rest of inputs those are after the one you selected will be selected too.
- Problem 2: if you shift-selected input b to input d, and then you unselect the input c, then again you hold shift key and select the input c, you'll get the others after input d will be selected too.

I guess the above two problems both are the same logic issues.

Since only has a seleted input equals the `checkbox === lastChecked` and some how it treats the last input as the `checkbox === this`, so it will iterate over all the rest of inputs (after the one we selected), and set the `inBetween = true` til the end.

### How to resolve this:

Here is one of the solutions I found on [stack overflow: How can I shift-select multiple checkboxes like GMail? ](http://stackoverflow.com/questions/659508/how-can-i-shift-select-multiple-checkboxes-like-gmail/659571#659571)

- Step 1: Turn the NodeList into an Array

```
const checkboxes = document.querySelectorAll('.inbox input[type="checkbox"]');
const checkboxesArray = [...checkboxes]; // This will turn the NodeList into an Array
```

- Step 2: When `e.shfitKey` is true, use `array.indexOf()` to get the index of selected inputs in the array to define the range (say the range contains the starting point like `checkbox === lastChecked` and the end point like `checkbox === this`)

```
let start = checkboxesArray.indexOf(lastChecked);
let end = checkboxesArray.indexOf(this);
```

- Step 3: `let` the `checkState` variable is `false`, it represents the inputs in the range which are checked or not

```
let checkState = false;
```

- Step 4: Use `array.slice()` to take all the elements between the range and change their `checkState` to checked

```
checkboxesArray
  .slice(Math.min(start, end), Math.max(start, end) + 1)
  .forEach(input => input.checked = checkState);
```

- Combine them all together:

```
const checkboxes = document.querySelectorAll('.inbox input[type="checkbox"]');
const checkboxesArray = [...checkboxes]; // Step 1

let checkState = false;  // Step 3
function handleCheck(e) {
  if(!lastChecked) { lastChecked = this; }  // mark the lastChecked to redefine the range
  checkState = lastChecked.checked ? true : false;  // checked or unchecked

  if(e.shiftKey) {
    // Step 2
    let start = checkboxesArray.indexOf(lastChecked);
    let end = checkboxesArray.indexOf(this);
    // Step 4
    checkboxesArray
      .slice(Math.min(start, end), Math.max(start, end) + 1)
      .forEach(input => input.checked = checkState);

    if(start - end < 0) {
      console.log(`from first selected input ${start} to second selected input ${end} are checked`);
    } else {
      console.log(`[Backforwad]form first selected input ${start} to second selected input ${end} are checked`);
    }
  }
  lastChecked = this;
}
```
