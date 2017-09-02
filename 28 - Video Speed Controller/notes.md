## 28 - Video Speed Controller

### Handle Move function

```
function handleMove(e) {
  const y = e.pageY - this.offsetTop;
  const percent = y / this.offsetHeight;
  const min = 0.4;
  const max = 4;
  const height = Math.round(percent * 100) + '%';
  const playbackRate = percent * (max - min) + min;
  bar.style.height = height;
  bar.textContent = playbackRate.toFixed(2) + 'x';
  video.playbackRate = playbackRate;
}
```

- `const y = e.pageY - this.offsetTop;`: Takes the offset where the top of the parent is located, and subtracts the offset from the y coordinate, which gives us just how much of the bar will be filled
- `const percent = y / this.offsetHeight;`: Calculates the height(%), divides Y by the total height of the parent, `y/offsetHeight` which will give us the decimal %

```
const min = 0.4;
const max = 4;
const height = Math.round(percent * 100) + '%';
```

- Defines the boundaries of `min` and `max`, and the height is equal to the percent multiplied by 100, which determines how much % of space will be filled by the `speed-bar`.

```
const playbackRate = percent * (max - min) + min;
```

- Find the number associated with that height and use it as the playback rate.  We use `percent * (max - min) + min` to match the playback rate, and assign it to the `video.playbackRate`

- `toFixed(2);` displays the number with 2 decimal places
