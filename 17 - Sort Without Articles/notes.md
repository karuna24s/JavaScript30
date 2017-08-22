## Part 17 - Sort Without Articles

### Sort data

Write in just one hot line

```
const sortedBands = bands.sort((a, b) => strip(a) > strip(b) ? 1 : -1);
```

which is equivalent to:

```
if(strip(a) > strip(b)) {
  return 1;
} else {
  return -1;
}
```

By default, it will sort by alphabetical order

### Strip out the words that we don't want

To strip out the specified words which are not articles:

```
function strip(bandName) {
  return bandName.replace(/^(a |the |an )/i, '').trim();
}
```

**[NOTICE]** we are only using `strip()` in a if statement, and we are not actually going to be modify our data (it's not necessary to do so)

then now it's sorted by alphabetical order after `strip()` the array

### Put them together

```
document.querySelector('#bands').innerHTML =
  sortedBands
    .map(band => `<li>${band}</li>`)
    .join('');
```

This takes the element and sets it to the `innerHTML`, and that's going to return an array with commas (`,`) by default, so we want to `join('')` it into one big string rather than a bunch of strings with commas in between

So we need to add 'join('')' to remove commas.
