## Part 27 - Click and Drag

### Define the variables that we need:

```
const slider = document.querySelector('.items');
let isDown = false;
let startX;
let scrollLeft;
```

- `isDown`: whether the mouse is clicked down or not
- `startX`: start point from the slider
- `scrollLeft`: store slider's scrollLeft when you scroll

### `mousedown()` function

1. Set the `isDown` to `true`
2. Add `active` class to the `slider`
3. Get the start point when mousedown
4. Get the previous `scrollLeft` when you scroll

```
slider.addEventListener('mousedown', (e) => {
  isDown = true;
  slider.classList.add('active');
  startX = e.pageX - slider.offsetLeft;
  scrollLeft = slider.scrollLeft;
});
```

- `isDown`: set `true` when mousedown
- `startX = e.pageX - slider.offsetLeft;`: prevent the initial starting point of the slider, which doesn't start from 0 (`offsetLeft`) of page (probably because of padding or margin around the slider), so we need to subtract the value of `slider.offsetLeft` to get the actual point of the position

### `mouseleave()` function

1. Set `isDown` back to `false`
2. Remove the `active` classList

```
slider.addEventListener('mouseleave', () => {
  isDown = false;
  slider.classList.remove('active');
});
```

### `mouseup()` function

1. Set `isDown` back to `false`
2. Remove the `active` classList

Same as `mouseleave()`

```
slider.addEventListener('mouseup', () => {
  isDown = false;
  slider.classList.remove('active');
});
```

### The `mousemove()` function

```
slider.addEventListener('mousemove', (e) => {
  if(!isDown) return;
  e.preventDefault();
  const x = e.pageX - slider.offsetLeft;
  const walk = (x - startX) * 3;
  // slider.scrollLeft = walk;
  slider.scrollLeft = scrollLeft - walk;
```

- `if(!isDown) return;`: Stop the function from running if not mousedown
- `e.preventDefault();`: Stop the browser from thinking that we might want to select the text

Small details:

- `const walk = (x - startX) * 3;`: how far we deviated from the initial point, and add with `* 3` (px) to make slider scroll smoothly

```
  // slider.scrollLeft = walk;
  slider.scrollLeft = scrollLeft - walk;
```

`slider.scrollLeft = walk;` seems to work but was still jumpy, so we recalculated to:
`slider.scrollLeft = scrollLeft - walk;` 
