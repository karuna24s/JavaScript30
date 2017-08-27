## Part 23 - Speech Synthesis

### Set up elements:

```
const msg = new SpeechSynthesisUtterance();
let voices = [];
const voicesDropdown = document.querySelector('[name="voice"]');
const options = document.querySelectorAll('[type="range"], [name="text"]');
const speakButton = document.querySelector('#speak');
const stopButton = document.querySelector('#stop');
msg.text = document.querySelector('[name="text"]').value;
```

### `populateVoices()` function:

```
function populateVoices() {
  voices = this.getVoices();  // get all the voices
  console.log(voices);

  // select dropdown
  voicesDropdown.innerHTML = voices
    // only want en ver. voices
    .filter(voice => voice.lang.includes('en'))
    .map(voice => `<option value="${voice.name}">${voice.name} (${voice.lang})</option>`)
    .join('');
}
```

- `console.log(voices)` will get all the voice synthesis

```
voices = this.getVoices();
console.log(voices);
```

- Select dropdown:

Since we only want just english versions, we can `filter` the array with `includes()`

```
voicesDropdown.innerHTML = voices
  .filter(voice => voice.lang.includes('en'))
  .map(voice => `<option value="${voice.name}">${voice.name} (${voice.lang})</option>`)
  .join('');
```

### `setVoice()` function:

Set the voice equals the value of the option that is selected

```
function setVoice() {
  msg.voice = voices.find(voice => voice.name === this.value);
  toggle();
}
```

### `toggle()` function:

Change voice while talking!  Remember to call this function in `setVoice()` and `setOption()`

```
function toggle(startOver = true) {
  speechSynthesis.cancel();
  if (startOver) {
    speechSynthesis.speak(msg);
  }
}
```

### `setOption()` function:

Changes the value of `Rate`, `Pitch` options and `textarea`

```
function setOption() {
  console.log(this.name, this.value);
  msg[this.name] = this.value;
  toggle();
}
```

### Hook up events:

```
speechSynthesis.addEventListener('voiceschanged', populateVoices);
voicesDropdown.addEventListener('change', setVoice);
options.forEach(option => option.addEventListener('change', setOption));
speakButton.addEventListener('click', toggle);
stopButton.addEventListener('click', () => toggle(false));
```
