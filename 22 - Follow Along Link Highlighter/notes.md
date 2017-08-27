## Part 22 - Follow Along Link Highlighter

### `createElement()` and `append()` it on to the DOM

```
const triggers = document.querySelectorAll('a');
const highlight = document.createElement('span');

highlight.classList.add('highlight');
document.body.append(highlight);
```

### `highlightLink()` function

```
function highlightLink() {
  const linkCoords = this.getBoundingClientRect();
  // console.log(this);  // <a> itself
  console.log(linkCoords);

  const coords = {
    width: linkCoords.width,
    height: linkCoords.height,
    top: linkCoords.top + window.scrollY,
    left: linkCoords.left + window.scrollX
  };

  highlight.style.width =`${coords.width}px`;
  highlight.style.height =`${coords.height}px`;
  highlight.style.transform = `translate(${coords.left}px, ${coords.top}px)`;
}

triggers.forEach(a => a.addEventListener('mouseenter', highlightLink));
```

**[NOTE]** need to add `window.scrollX` and `window.scrollY` to see the  right position while we scroll

```
top: linkCoords.top + window.scrollY,
left: linkCoords.left + window.scrollX
```
### Setting initial start coordinates:

because we don't want it to "slide" in from the `(X,Y) = (0,0)` of the window's coordinates, so let's set it from the first `<li>` element of `<nav>`

```
const initStart = {
  left: initCoord.left + window.scrollX,
  top: initCoord.top + window.scrollY
};

highlight.style.transform = `translate(${initStart.left}px, ${initStart.top}px)`;
```
