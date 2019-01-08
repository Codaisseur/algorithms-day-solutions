Example solution, using immutability and functional style:

```js
function jsonfilter(data) {
  if (Array.isArray(data)) {
    return data
      .filter(item => typeof item !== 'string')
      .map(jsonfilter);
  } else {
    return data;
  }
}
```