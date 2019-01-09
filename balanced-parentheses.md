The proposed function signature of the solution points you in the right direction. After looking at the whole string, we need to have a balanced number of opening and closing brackets. So, the open count should end up being zero. However, at no point is the open count allowed to be negative.

```js
function balance(letters, index=0, openParensCount=0) { 
  if (index === letters.length) {
    return openParensCount === 0
  }
  if (letters[index] === '(') {
    openParensCount++
  } else if(letters[index] === ')') {
    openParensCount--
  }
  if (openParensCount < 0) {
    return false
  }
  return balance(letters, index + 1, openParensCount)
}
```


# Different brackets
Here is a more sophisticated solution that works for different types of brackets.

```js
// A reference object to easily find the opening bracket by it's closing character.
const openingBrackets = {
    "}": "{",
    ")": "(",
    "]": "[",
}

/*
The parameter `string` is the input that we're checking.
The parameter `i` is the current character in the string that we're inspecting.
Lastly, `open` is an array containing all the brackets that are open an haven't been closed yet.
*/
function isBalanced(string, i, open) {
    open = open || [] // if open is undefined, it should default to an empty array
    i = i || 0 // if i is undefined, it should default to 0
    if (i >= string.length) {
        // if we've reached the end of the string and there are no more open brackets
        // then the string is balanced
        return open.length === 0
    }
    // Conditional that checks what the current character is
    switch (string[i]) {
        // If it matches any of the opening brackets...
        case '(':
        case '[':
        case '{':
            // remember that it's opened and proceed
            open.push(string[i])
            break;
        // If it's any of the closing brackets
        case ')':
        case '}':
        case ']':
            // Validate that the currently opened bracket is of the same type as this closing bracket
            if (open[open.length - 1] !== openingBrackets[string[i]]) {
                return false
            }
            // remove the last item from the open array
            open.pop()
            break;
        // ignore all other characters
        default:
            break;
    }
    // Check the next location in the string
    return isBalanced(string, i + 1, open)
}

const testCases = [
    ['[]{}()', true],
    ['(if (zero? x) max (/ 1 x))', true],
    ['())(', false],
    [':-)', false]
]

for (let testCase of testCases) {
    console.log(`The test case '${testCase[0]}' passes: ${isBalanced(testCase[0]) === testCase[1]}`)
}
```