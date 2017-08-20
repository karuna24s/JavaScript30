## Part 14 - JavaScript References VS Copying

### Strings, Numbers and Booleans reference and copy

```
let age = 100;
let age2 = age;
age2 = 200;

let name = 'Kyle';
let name2 = name;
name2 = 'Chad';
```

### Arrays reference and copy

```
let players = ['Wes', 'Sarah', 'Ryan', 'Poppy'];
const team = players;
```

If we update the `team[3]`

```
team[3] = 'Chad';
```

that will also update the `players[3]` too, and that is not what we want

To fix it, we take a copy instead

```
const team2 = players.slice();
const team3 = [].concat(players); // same way as team2

team2[3] = "Chad";
team3[3] = "Chad";
```

So that way it won't change the original one (players)

You can also use ES6 spread syntax

```
const team4 = [...players];   // just like take a copy
team4[3] = "Hello Kitty~ Meow";
```

or you can use `Array.from()` as well

```
const team5 = Array.from(players);  // same as team4
team5[3] = "Hello Kitty~ Meow";
```


### Objects reference and copy

We make a copy of `person` object and want to add `number` property to only `captain` object

```
const person = {
  name: "Tom",
  age: 30
};

const captain = person;
captain.number = 100;
```

Will it also change the `person` object ?

unfortunately ...yes, and that's not what we want

we can use [`Object.assign()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) to fix this

- `Object.assign()`: first argument is an empty object (`{}`), second is the object (`person`) to fold in, third are the values we want to additionally fold in (`{ number: 100 }`)

```
const man2 = Object.assign({}, person, { number: 100 });
```

but there's a problem the **`Object.assign()` only copy is one level deep**... so if you try:

```
const tom = {
  name: 'Tom',
  age: 30,
  social: {
    twitter: '@tomyes',
    facebook: 'tomyes.coolman'
  }
};

const tom2 = Object.assign({}, tom);
tom2.social.twitter = '@tom2_nobody';
```

The `tom.social.twitter` will change as well

If we need to get a clone deep (i.e. second level deep), we have to run a function called **clone deep** and that will clone every level as deep as you want. and before doing it, we might ask ourselves that do we really need to do this?

There is some another way to do a clone deep by using `JSON.parse(JSON.stringify())`, just pass in the `tom` like:

```
const tom3 = JSON.parse(JSON.stringify(tom));
tom3.social.twitter = '@tom3_nobody';
```

so the `tom.social.twitter` won't be changed

we can `console.log()` through the `JSON.stringify()` to turn the `tom` object into a `string` and then pass it to `JSON.parse()` to construct into an `object`

- THe [`JSON.stringify()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify) methods converts a JavaScript value to a JSON string

- The [`JSON.parse()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse) method parses a JSON string, constructing the JavaScript value or object described by the string
