## Part 15 - LocalStorage and Event Delegation

`localStorage`, `e.preventDefault()`

### Take and load data with localStorage

```
const addItems = document.querySelector('.add-items');
const itemsList = document.querySelector('.plates');
const items = JSON.parse(localStorage.getItem('items')) || [];
// const items = [];
```

`const items` checks if there is something in `localStorage` and then we fall back to an empty array

- The [`localStorage`](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage) property allows you to access a localStorage object

```
function addItem(e) {
  e.preventDefault();

  const item = {
    text: text,  // or in ES6 syntax: `text,`
    done: false
  };

  items.push(item);
  populateList(items, itemsList);
  // localStorage.setItem ('items', items);
  localStorage.setItem ('items', JSON.stringify(items));
  this.reset();
}
```

- [`e.preventDefault()`](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault) -> cancels the event if it is cancelable, without stopping further propagation of the event
- `items.push(item);` -> takes `item` and puts it into the `items` array
- `this.reset();` -> `this` is the `form`, `reset()` is the form method to clear the input

**[NOTICE]**

```
localStorage.setItem ('items', items);`
```

will just get `string` as return

that's because the browser doesn't know how to handle it so it will use `toString()` method which exists on the number or the object (in this case is an array), therefore what we need to do is to `JSON.stringify()` it before we convert like so

```
localStorage.setItem ('items', JSON.stringify(items));
```

### Update the view part

Use `populateList()` as this way is much more resilient than just reaching outside the items and grabbing them the place where we will dump them

- The `populateList()` needs two things:
  - A list of plates to populateList: `plates = []`
     - Don't forget to set the default `plates` as an empty array(or object), otherwise it will break up the javascript sometimes (in this case the `plates` is an array)
  - A place to put the HTML: `plateList`

```
function populateList(plates = [], plateList) {
  plateList.innerHTML = plates.map((plate, i) => {
    return `
      <li>
        <input type="checkbox" data-index=${i} id="item${i}" ${plate.done ? 'checked' : ''}>
        <label for="item${i}">${plate.text}</label>
      </li>
    `
  }).join('');
}
```

Here the `.join('')` takes the array (which is where `places.map()` is made) and turn into a string and then pass it to `innerHTML`

### Toggle the checked status

```
function toggleDone(e) {
  if(!e.target.matches('input')) return;

  const el = e.target;
  const index = el.dataset.index;

  items[index].done = !items[index].done;
  localStorage.setItem ('items', JSON.stringify(items))
  populateList(items, itemsList);
}
```

Let's take look:

- Skip this unless it's an input

```
if(!e.target.matches('input')) return;
```

- Flip-flopping between true and false

```
items[index].done = !items[index].done;
```

- Every time the update will mirror to the localStorage

```
localStorage.setItem ('items', JSON.stringify(items));
```

- And will uppdate the actual visibility part on html

```
populateList(items, itemsList);
```

### Hook up events and update visibility part on page

```
addItems.addEventListener('submit', addItem);
itemsList.addEventListener('click', toggleDone);
populateList(items, itemsList);
```

### Extended thinking

Every time we create an item, it calls `populateList()` and rerenders the entire list again instead of updating one single line, in this case this is OK on performance, but practically just updating one single line by using React or other frameworks is more efficient and helpful
