Like in step 2, it makes more sense to start with `word` and ask something like *"are all its letters guessed?"*. It doesn't really make a lot of sense to start with `guesses`.

```js
function isWinner(word, guesses) {
  // checks whether all letters have been guessed
  return word
    .split('')
    .filter(letter => guesses.indexOf(letter) >= 0)
    .length === word.length;
}
```
