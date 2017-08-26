## Part 21 - Geolocation

### Basic Geolocation

The [`Geolocation.watchPosition()`](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation/watchPosition) method is used to register a handling function that will be called automatically each time the position of the device changes. You can also, optionally, specify an error handling callback function.

```
const arrow = document.querySelector('.arrow');
const speed = document.querySelector('.speed-value');

navigator.geolocation.watchPosition(function(data) {
  // success callback
  // console.log(data);
  speed.textContent = data.coords.speed;
  arrow.style.transform = `rotate(${data.coords.heading}deg)`;
  // error callback
}, function(err) {
  console.log(err);
  alert('Oh NO...you gotta allow that to happen!!');
});
```

##### success

```
function(data) {
  speed.textContent = data.coords.speed;
  arrow.style.transform = `rotate(${data.coords.heading}deg)`;
}
```

##### error

```
function(err) {
  console.log(err);
  alert('Oh NO...you gotta allow that to happen!!');
}
```
