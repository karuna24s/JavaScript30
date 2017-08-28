# 25 - Event Capture, Propagation, Bubbling and Once

`e.stopPropagation()`, `capture`, `once`

### `event.stopPropagation()`

The [`event.stopPropagation()`](https://developer.mozilla.org/en-US/docs/Web/API/Event/stopPropagation) prevents further propagation of the current event in the capturing and bubbling phases.

To bubble up which means that it's triggering that event as you go up, so use `e.stopPropagation();` to stop bubbling that event up.

```
function logText(e) {
  console.log(this.classList.value);
  e.stopPropagation();
}

document.body.addEventListener('click', logText);
divs.forEach(div => div.addEventListener('click', logText));
```

### The `capture` and `once`

refernce: [here -> EventTarget.addEventListener()](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)

##### `capture`

`capture` is a boolean that indicates that event of this type will be dispatched to the registered listener before being dispatched to any EventTarget beneath it in the DOM tree.

```
function logText(e) {
  console.log(this.classList.value);
}

divs.forEach(div => div.addEventListener('click', logText, {
  capture: false
}));
```

##### `once`

`once` is a boolean indicating that the listener should be invoked at most once after being added. **If it is true, the listener would be removed automatically when it is invoked**.

```
button.addEventListener('click', () => {
  console.log('Click!!!');
}, {
  once: false
});
```
