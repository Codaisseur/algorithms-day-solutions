You are asked to calculate the average length of a stretch of road in a route, in kilometers, using the provided code.

Since the average length, is the total length divided by the number of roads, we end up with:

```js
const route1 = [2.1, 3.5, 0.3, 5.2]

function total(route) {
  let res = 0
  for (let i = 0; i < route.length; i++) {
    res += route[i]
  }
  return res
}

function averageStretch(route) {
  return total(route) / route.length
}

console.log('average kilometers per stretch:', averageStretch(route1))
```
