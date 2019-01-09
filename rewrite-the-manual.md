The provided code uses for-loops. Now, using `map`, `filter`, and `reduce` they will look something like this:

```js
// No changes here:
const route1 = [2.1, 3.5, 0.3, 5.2]
function kilometerToMile(km) {
  return km / 1.6
}


function routeInMiles(route) {
  return route.map(kilometerToMile)
}

// test
console.log(JSON.stringify(routeInMiles(route1)))

function longStretches(route) {
    return route.filter(r => r > 2)
}

// test
console.log(JSON.stringify(longStretches(route1)))


function total(route) {
    return route.reduce((acc, length) => acc + length, 0)
}

// test
console.log(total(route1) === 11.1)
```

Implementing your own version of `map`, `filter`, and `reduce` could look something like this:

```js
function map(array, mapper) {
    const result = []
    for (const item of array) {
        result.push(mapper(item))
    }
    return result
}

function filter(array, predicate) {
    const result = []
    for (const item of array) {
        if (predicate(item)) {
            result.push(item)
        }
    }
    return result
}

function reduce(array, reducer, initialValue) {
    let result = initialValue
    for (const item of array) {
        result = reducer(result, item)
    }
    return result
}
```

Interestingly, it's possible to implement `map` and `filter` using reduce:

```js
function map(array, mapper) {
    return reduce(array, (acc, val) => acc.concat([mapper(val)]), [])
}

function filter(array, predicate) {
    return reduce(array, (acc, val) => predicate(val) ? acc.concat([val]) : acc, [])
}
```