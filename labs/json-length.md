First, if you're unsure about JSON (what's valid and not, how data is serialized, etc.), go take a look at the [JSON spec](https://www.json.org/). The "railway diagrams" explaining the syntax are very clear. *(Also, don't worry for now about all the complications with escaped characters and scientific number formats etc. The idea of the exercise is to understand recursion, not to understand the JSON spec in its entirety.)*

This is an exercise in using recursion. Remember, a recursive function has two key aspects:

* One or more **base cases**. These are very important, and it often helps to think of these simple cases first.
* A method of breaking "larger" problems (inputs) into "smaller" problems (inputs).

For our situation, inputs are "large" if they are objects or arrays, and "small" if they are primitive data types: a string, number, boolean, or `null`. *(Interestingly, JSON does not have an `undefined` type.)*

So, our base cases are:

| Base case | Example | Length |
|---|---|---|
| String | `x = "hello"` | The length of the string, plus the quotation marks:<br /><br /> `x.length + 2` |
| Boolean | `x = true` | Either 4 letters for `true` or 5 letters for `false`, so:<br /><br /> `x ? 4 : 5` |
| Null | `x = null` | Just `null`, so:<br /><br /> `4` |
| Number | `x = -3.14` | This is actually quite hard. The 10-log of 0 is not defined / minus infinity, so that's an edge-case. Also, you can only apply `Math.log10` to non-negative numbers. Also, remember to round UP the result of `Math.log10`, and to include 1 letter for the minus sign if the number is negative. See below. |

Now to the "larger" inputs are objects and arrays. Running some quick checks to understand how JSON serializes, we get:

```js
console.log(JSON.stringify([42, "hello", false]));
// [42,"hello",false]

console.log(JSON.stringify({ hello: "world" }));
// {"hello":"world"}
```

We've learned two things: (1) JSON strips away all white-spaces in between values (they're unnecessary anyway), and (2) the keys of an object are surrounded in quotation marks as well.

Now we should know enough to build our recursive function. Also: don't hesitate to write partial implementations along the way, for testing purposes! For example, checking your first base-case(s) works perfectly well without the recursive part, so an intermediate implementation might look like:

```js
function jsonlength(data) {
  if (typeof data === 'number') {
    if (data === 0) {
      return 0; // Because `Math.log(0) === -Infinity`
    }
    else {
      const positive = Math.abs(data);
      const numDigits = Math.ceil(Math.log10(positive + 1));
      return numDigits + (data < 0 ? 1 : 0); // minus sign
    }
  }
  else {
    console.log('TODO');
  }
}
```

In fact, because it turns out that dealing with the number is quite hard, we might want to split that piece of logic into a separate function for easier testing:

```js
function numberLength (data) {
  if (data === 0) {
    return 0; // Because `Math.log(0) === -Infinity`
  }
  else {
    const positive = Math.abs(data);
    const numDigits = Math.ceil(Math.log10(positive + 1));
    return numDigits + (data < 0 ? 1 : 0); // minus sign
  }
}

// some test-cases
console.log(numberLength(123));
console.log(numberLength(-123));
console.log(numberLength(0));
console.log(numberLength(1));
console.log(numberLength(10));
```

Here's a full implementation:

```js
function jsonlength(data) {
  if (typeof data === 'number') {
    return numberLength(data);
  }
  else if (typeof data === 'string') {
    return data.length + 2;
  }
  else if (typeof data === 'boolean') {
    return data ? 4 : 5;
  }
  else if (data === null) {
    return 4;
  }
  else if (Array.isArray(data)) {
    const entry_lengths_total = data.map(jsonlength).reduce((a, b) => a + b);
    // add two brackets, and commas between the values
    // (but if the array is empty, no commas at all)
    return 2 + entry_lengths_total + (data.length === 0 ? 0 : data.length - 1);
  }
  else {
    const entries = Object.entries(data);
    // the same as above, except we add the keys as well, and
    //  a `:` between each key and value
    const entry_lengths_total = entries
      .map(([key, val]) => {
        return jsonlength(key) + 1 + jsonlength(val);
      })
      .reduce((a, b) => a + b);
    
    return 2 + entry_lengths_total + (data.length === 0 ? 0 : data.length - 1);
  }
}
```