## Part 19 - Unreal Webcam Fun


For accessing our webcam, it must be tied to *secure origin*, this means that a website is `HTTPS`, and `localhost` in our tutorial is also a secure origin. We use `npm` (`npm install` & `npm start`) to run our small server to build the page.

### To `querySelector` elements we need:

```
const video = document.querySelector('.player');
const canvas = document.querySelector('.photo');
const ctx = canvas.getContext('2d');
const strip = document.querySelector('.strip');
const snap = document.querySelector('.snap');
```

### `getVideo()` function:

First of all, we need to get the real video source:

```
function getVideo() {
  navigator.mediaDevices.getUserMedia({ video: true, audio: false })
    .then(localMediaStream => {
      console.log(localMediaStream);
      video.src = window.URL.createObjectURL(localMediaStream);
      video.play();
    })
    .catch(err => {
      console.error(`OH NO!!!`, err);
    });
}

```

The `.catch` is to handle the error.

Check out the HTML page and you will see that the `video`'s `src` is a `blob: http://XXX`. `blob` means that a *raw data* is being piped off this webcam right on the page.

### `paintToCanvas()` function

Take a frame from the video (on the upper-right corner), and paint it onto the actual canvas right on the page

```
function paintToCanvas() {
  const width = video.videoWidth;
  const height = video.videoHeight;
  canvas.width = width;
  canvas.height = height;

  return setInterval(() => {
    ctx.drawImage(video, 0, 0, width, height);
    // take the pixels out
    let pixels = ctx.getImageData(0, 0, width, height);

    // try some effects
    // pixels = redEffect(pixels);

    pixels = rgbSplit(pixels);
    // ctx.globalAlpha = 0.8;

    // pixels = greenScreen(pixels);
    // put them back
    ctx.putImageData(pixels, 0, 0);
  }, 16);
}
```

Make sure that the canvas's width and height equals the webcam's width and height to render properly:

```
const width = video.videoWidth;
const height = video.videoHeight;
canvas.width = width;
canvas.height = height;
```

### `takePhoto()` function, call `getVideo()` function, and add an eventListener:

```
function takePhoto() {
  // played the sound
  snap.currentTime = 0;
  snap.play();

  // take the data out of the canvas
  const data = canvas.toDataURL('image/jpeg');
  const link = document.createElement('a');
  link.href = data;
  link.setAttribute('download', 'snapshot');
  link.innerHTML = `<img src="${data}" alt="snap shot" />`;
  strip.insertBefore(link, strip.firsChild);
}

getVideo();

video.addEventListener('canplay', paintToCanavas);

```
