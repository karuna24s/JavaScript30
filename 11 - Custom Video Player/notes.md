## Part 11 - Custom Video Player

`video.paused`, `video.currentTime`, `dataset` of `.data-` attribute, `parseFloat()`

### Get all the elements we need

Use `.querySelector` or `.querySelectorAll` to get the elements we need to build up the panel for video player

```
const player = document.querySelector('.player');
const video = document.querySelector('.viewer');
const progress = document.querySelector('.progress');
const progressBar = document.querySelector('.progress__filled');
const toggle = document.querySelector('.toggle');
const skipButtons = document.querySelectorAll('[data-skip]');
const ranges = document.querySelectorAll('.player__slider');
```

### Build out functions

- function togglePlay()
  - Click the on video to play
  - `.paused` is the property of `video`

  and there is no `.playing` property live on `video`

  ```
  function togglePlay() {
    const method = video.paused ? 'play' : 'pause';
    video[method]();
  }
  ```

  and another approach is:

  ```
  if(video.paused) {
    video.play();
  } else {
    video.pause();
  }
  ```

- function updateButton()
  - Toggle the play button during the video plays or pauses

  In order to change icon, you have to change the `textContent` property

  ```
  const icon = this.paused ? '►' : '❚ ❚';  // `this` is the `video`
  toggle.textContent = icon;
  console.log({toggle});  // log the `{toggle}` out to see where the `textContent` is
  ```

- function skip()
  - Click the skip buttons to skip

  The two skip buttons are: `<button data-skip="-10"></button>` and `<button data-skip="25"></button>`

  ```
  console.log(this.dataset.skip);
  video.currentTime += parseFloat(this.dataset.skip);
  ```
  `console.log(this.dataset)` can get the information which is the value we just added as `data-skip` attribute on HTML.

  then we use its `skip` property and `parseFloat` to change it into a float number to `-10s` or `+25s`.

- function handleRangeUpdate()
  - Handle the two input sliders

  The two input sliders are: `<input type="range" name="volume">` and `<input type="range" name="playbackRate">`

  ```
  console.log(`${this.name}: ${this.value}`);
  video[this.name] = this.value;
  ```

  The `name` of `this.name` is the `volume` or `playbackRate`, which is what we define the `name` attributes of the inputs in the HTML file.

- function handleProgress()
  - Updates the progress bar when the video plays

  `percent` defines the width of `progressBa`r's `flexBasis`

  ```
  const percent = (video.currentTime / video.duration) * 100;
  progressBar.style.flexBasis = `${percent}%`;
  console.log(percent);
  ```

- function scrub(e)
  - Changes the progress bar width when we want drag or click on it

  Add `console.log(e)` to check the `MouseEvent` out and you will find the `offsetX` which is relative to the progress `offsetWidth`, use them to calculate the `scrubTime` and then update the video's `currentTime`

  ```
  const scrubTime = (e.offsetX / progress.offsetWidth) * video.duration;
  video.currentTime = scrubTime;
  console.log(e);
  ```

### Hook up the event listeners

- Click on the video to play

  ```
  video.addEventListener('click', togglePlay);
  ```

- Toggle the play button icon when the video plays or pauses

  ```
  video.addEventListener('play', updateButton);
  video.addEventListener('pause', updateButton);
  ```

- Update the progress bar when the video plays

  ```
  video.addEventListener('timeupdate', handleProgress);
  ```

- Toggle the play button to play or pause

  ```
  toggle.addEventListener('click', togglePlay);
  ```

- Click to skip (to `-10s` or `+25s`)

  ```
  skipButtons.forEach(button => button.addEventListener('click', skip));
  ```

- Handle range input sliders

  add `mousemove` event for updating real-time, rather than when just we let go of the button

  ```
  ranges.forEach(range => range.addEventListener('change', handleRangeUpdate));
  ranges.forEach(range => range.addEventListener('mousemove', handleRangeUpdate));
  ```

- Change the progress bar width when we click on or drag it.

  ```
  progress.addEventListener('click', scrub);
  ```
