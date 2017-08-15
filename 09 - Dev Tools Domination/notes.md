## Part 9 - Dev Tools Domination

`Attributes Modification` on an element and bunch of `console` tricks

### Attributes Modification

Makes a break point to see what's going on to the element.

### Dominating the `console` tricks

- More `console.log`
  - We most commonly use `console.log();`
  - You can also use intropolation as well:
    - `%s`: string

      `console.log("Hi %s!", "girl"); // Hi girl!`

    - `%d`: integer

      `console.log("I am %d years old!", 25);  // I am 25 years old!`
    - `%f`: float

      `console.log("It's %f euros.", 23.5);  // It's 23.5 euros.`

    - `%o`: object

      `console.log("This is an object:  %o", {firstName: 'Amber', lastName: 'Simpson', age: 20});`

    - `%c`: for styled
      `console.log("I am not just a log, I am %c CONSOLE DOT LOG!!", "font-size: 18px;color: blue;background-color: yellow");`


- defaults of `console.log`
  - `console.warn` for warning message

    `console.warn("← a warning sign %c Watch out! ", "background-color: #eeaf1e;color: #fff");`

  - `console.error` for error message

    `console.error("← an error sign %c Oh Darn! ", "background-color: red;color: #fff");`

  - `console.info` for info message

    `console.info("← an info sign %c Practice makes perfect! ", "background-color: #274ed0;color: #fff");`


- Testing with `assert()`
  - Nothing returns if true

    `console.assert(1 === 1, "Hey it\'s true"); // nothing returns`

  - Returns the second argument if false

    `console.assert(1 === 0, "Hey you\'re wrong!"); // Hey your're wrong!`

  - Use `assert()` to check DOM element

    ```
    const p = document.querySelector('p');
    console.log("3. you can also check the DOM or something");
    console.assert(p.innerHTML.match('Break'), "There is no \'Break\' in <p> here, try \'BREAK\'");
    ```


- Viewing DOM elements
  - `document.querySelector()` an element first
  - Log out only a DOM tag of the element

    `console.log(p);`

  - Use `console.dir()` to view the properties of the element

    `console.dir(p);`


- Log out something, like an array with console.table(), which provides a cleaner look:
  - Simply `console.table()` all out

    `console.table(dogs);`

  - `console.table()` specifies things out

    `console.table(dogs, ['age']);`



- Grouping together

`group()`/`groupCollapsed` and `groupEnd()` will automatically group things up

  ```
  const dogs = [{ name: 'Snickers', age: 2 }, { name: 'hugo', age: 8 }];
  dogs.forEach(dog => {
    console.group();                // open up the group
    // console.groupCollapsed();    
    console.log(`${dog.name}`);
    console.log(`${dog.age}`);
    console.log(`${dog.name} is ${dog.age} years old.`);
    console.groupEnd();             // close up the group
  });
  ```


- Counting things

Counts only contents inside of `console.count()`

  ```
  console.count("chcolate");
  console.count("candy");
  console.count("chcolate");
  console.count("candy");
  console.count("chcolate");
  console.count("potato chips");
  console.count("chcolate");
  ```


- Processing times

`time('name')` controls the start point and `timeEnd('name')` controls the end point, the `'name'` variables are what we define and must be the same.

```
console.time('fetching data');
fetch('http://api.github.com/users/amelieyeh')
  .then(data => data.json())
  .then(data => {
    console.timeEnd('fetching data');
    console.log(data);
  });
```


### Clearing the console

There are two ways to clear the console:

- `console.clear();`
- hit `Ctrl + L` (in Chrome)
