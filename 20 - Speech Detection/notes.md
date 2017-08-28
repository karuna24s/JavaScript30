## Part 20 - Speech Detection

In order to open 20 - Speech Detection in Terminal, change the name of the directory to 20SpeechDetection.

### `SpeechRecognition`

```
window.SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;

const recognition = new SpeechRecognition();
recognition.interimResults = true;
```
- [`window.SpeechRecognition`](https://developer.mozilla.org/en-US/docs/Web/API/SpeechRecognition) is a `Web Speech API`.

- `recognition.interimResults = true;` makes sure that results are available while we are speaking

```
let p = document.createElement('p');
const words = document.querySelector('.words');
words.appendChild(p);
```
- Use `document.createElement` to create a paragraph and `append` it to the `.words` div

### Add transcripts

```
recognition.addEventListener('result', e => {
  const transcript = Array.from(e.results)
    .map(result => result[0])
    .map(result => result.transcript)
    .join('');

    const poopScript = transcript.replace(/poop|poo|shit|dump/gi, '💩');
    p.textContent = poopScript;

    if (e.results[0].isFinal) {
      p = document.createElement('p');
      words.appendChild(p);
    }
});

recognition.addEventListener('end', recognition.start);

recognition.start();
```

- Add an `eventListener` on `result` event of SpeechRecognition, in the event we will get `e.results` and assign to the `transcript` variable.

- `e.results` is a list **NOT** an array

- Each `0th` element of the list is the text data we need, so we have to `map` transcript on `result[0]`

- Return `transcript` and `join` everything so that it forms a single string.

- This only works for one paragraph so we need to set `recognition.addEventListener('end', recognition.start)` again.

- To avoid the `<p>` getting replaced in the DOM, we need to run `createElement` and `appendChild` inside the `result` event again so that it creates a new paragraph instead.
