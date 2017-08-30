## 26 - Stripe Follow Along Nav

### `handleEnter()` function

```
function handleEnter() {
  this.classList.add('trigger-enter');
  setTimeout(() => this.classList.contains('trigger-enter') && this.classList.add('trigger-enter-active'), 150);

  background.classList.add('open');

  const dropdown = this.querySelector('.dropdown');
  const dropdownCoords = dropdown.getBoundingClientRect();
  const navCoords = nav.getBoundingClientRect();

  const coords = {
    height: dropdownCoords.height,
    width: dropdownCoords.width,
    top: dropdownCoords.top - navCoords.top,
    left: dropdownCoords.left - navCoords.left
  };

  background.style.setProperty('width', `${coords.width}px`);
  background.style.setProperty('height', `${coords.height}px`);
  background.style.setProperty('transform', `translate(${coords.left}px, ${coords.top}px)`);
}
```

- The `setTimeout()` occurs if it has `trigger-enter` class and it equals true then it will execute `this.classList.add('trigger-enter-active')` , it will prevent the weird `trigger-enter-active` when you hover quickly between li items

```
setTimeout(() => this.classList.contains('trigger-enter') && this.classList.add('trigger-enter-active'), 150);
```

The code shown above uses an  ES6 arrow function to properly inherit from it's parent instead, otherwise `this` will be the `window` and will throw an error

- Figure out the nav's position as initial coords

```
const navCoords = nav.getBoundingClientRect();
```

- To prevent wrong position when the nav has be pushed down or moved offset on X-asis, so `- navCoords.`top/left

```
top: dropdownCoords.top - navCoords.top,
left: dropdownCoords.left - navCoords.left
```

### `handleLeave()` function

```
function handleLeave() {
  this.classList.remove('trigger-enter', 'trigger-enter-active');
  background.classList.remove('open');
}
```

### Hook up events

```
triggers.forEach(trigger => trigger.addEventListener('mouseenter', handleEnter));
triggers.forEach(trigger => trigger.addEventListener('mouseleave', handleLeave));
```
