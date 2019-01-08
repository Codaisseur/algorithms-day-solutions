The main idea here, is that you only need a single `reduce`. Here's an implementation that demonstrates this:

```js
function countTypes(data) {
  return data.reduce((totals, item) => {
    if (typeof item === 'string') {
      totals.strings++;
    } else if (typeof item === 'number') {
      totals.numbers++;
    } else if (item === null) {
      totals.nulls++;
    } else {
      console.log('ERROR');
    }
    return totals;
  }, {
    numbers: 0,
    strings: 0,
    nulls: 0,
  });
}
```

Even better though, would be an implementation that doesn't mutate the `totals` object. Luckily, the new JavaScript spread syntax allows us to do this quite eloquently, as follows:

```js
function countTypes(data) {
  return data.reduce((totals, item) => {
    if (typeof item === 'string') {
      return { ...totals, strings: totals.strings + 1 };
    }
    else if (typeof item === 'number') {
      return { ...totals, numbers: totals.numbers + 1 };
    }
    else if (item === null) {
      return { ...totals, nulls: totals.nulls + 1 };
    }
    else {
      return 'ERROR';
    }
  }, {
    numbers: 0,
    strings: 0,
    nulls: 0,
  });
}
```
