## Part 15 - CSS Text Shadow Mouse Move Effect

### Grab elements and hook up mousemve event

We hooked up `mousemove` event on the `hero` element, and we want to do text shadow effect on its text, right in the `h1` tag.

```
const hero = document.querySelector('.hero');
const text = hero.querySelector('h1');

hero.addEventListener('mousemove', shadow);
```

### The shadow function

`walk` is defined to calculate the space between shadows, the more higher the value is, the spacing is more bigger

```
const walk = 500;  // 500px
```

set the `width` and `height` of `hero`

in ES6 syntax

```
const { offsetWidth: width, offsetHeight: height } = hero;
let { offsetX: x, offsetY: y } = e;
```

```
const width = hero.offsetWidth;
const height = hero.offsetHeight;
let x = e.offsetX;
let y = e.offsetY;
```

By adding a `console.log()` we will see that `this` is `.hero` and `e.target` is `h1`

```
console.log(this, e.target);
```

Calculate offset positions:

```
if(this !== e.target) {
  x = x + e.target.offsetLeft;
  y = y + e.target.offsetTop;
}

const xWalk = Math.round((x / width * walk) - (walk / 2));
const yWalk = Math.round((y / height * walk) - (walk / 2));
console.log(xWalk, yWalk);
```

Add a console.log with the `xWalk` and `yWalk` variables in order to see the offsets after calculating

and for the CSS part, add the `textShadow` effect

```
text.style.textShadow = `
  ${xWalk}px ${yWalk}px 0 rgba(255, 0, 255, 0.7),
  ${xWalk * -1}px ${yWalk}px 0 rgba(0, 255, 255, 0.6),
  ${yWalk}px ${xWalk * -1}px 0 rgba(0, 255, 0, 0.5),
  ${yWalk * -1}px ${xWalk}px 0 rgba(0, 0, 255, 0.4)
`;
```

- The [`offsetLeft`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/offsetLeft)  property returns the number of pixels that the **upper left** corner of the current element is offset to the left within the [`.offsetParent`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLelement/offsetParent) node.

- The [`offsetTop`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/offsetTop) property returns the distance of the current element relative to the **top** of the [`offsetParent`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLelement/offsetParent) node.
