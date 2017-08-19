## Part 13 - Slide in on Scroll

`window.scrollY`, `window.innerHeight`, `offsetTop`

### Debouncing

Use the debounce function provided in the exercise, to avoid performance issues. Just wrap the `checkSlide` function into the `debounce()` function

```
window.addEventListener('scroll', debounce(checkSlide));
```

### Checking images

```
function checkSlide(e) {
  sliderImages.forEach(sliderImage => {

    // half way through the image
    const slideInAt = (window.scrollY + window.innerHeight) - sliderImage.height / 2;

    // bottom of the image
    const imageBottom = sliderImage.offsetTop + sliderImage.height;

    const isHalfShown = slideInAt > sliderImage.offsetTop;
    const isNotScrolledPast = window.scrollY < imageBottom;

    if(isHalfShown && isNotScrolledPast) {
      sliderImage.classList.add('active');
    } else {
      sliderImage.classList.remove('active');
    }
}
```

The `.offsetTop` tells us that the top of image is how far from the top of the actual window.
