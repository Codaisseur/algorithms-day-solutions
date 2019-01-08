Of course this is an exercise in using recursion. We already have an implementation that counts numbers, strings, and nulls. We just need to *extend* it to also do something with arrays. When we encounter an array, we just call the function *recursively*, and then include these sub-totals in the total counts:

```js
function countTypesNested(data) {
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
    else if (Array.isArray(item)) {
      let item_totals = countTypesNested(item);
      return {
        numbers: totals.numbers + item_totals.numbers,
        strings: totals.strings + item_totals.strings,
        nulls: totals.nulls + item_totals.nulls,
        // note the `+1` to count `item` itself as wells
        arrays: totals.arrays + 1 + item_totals.arrays,
      };
    }
    else {
      return 'ERROR';
    }
  }, {
    numbers: 0,
    strings: 0,
    nulls: 0,
    arrays: 0,
  });
}
```