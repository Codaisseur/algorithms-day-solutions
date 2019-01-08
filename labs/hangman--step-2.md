Again, we have a "one-liner" solution using functional style:

```js
function showGuess(word, guesses) {
  return word
    // first split the word into letters
    .split('')
    // for each letter, transform it to an understore
    //  if it was not guessed, or else leave it untouched
    .map(letter => guesses.indexOf(letter) < 0 ? '_' : letter)
    // then join the letters/underscores back together,
    //  but with some extra spacing between each
    .join(' ');
}
```

Note that where in step 1, we started out with `guesses`, and then did a `filter` on it and check the resulting `length`, now we've started out with `word`, subsequently doing a `split`, then a `map`, then `join`ing it back together. This is because in the step 1, we were *asking a question about `guesses`*, and now we're *asking a question about the letters in `word`*. So it's a natural choice to start out with `word`.

For completeness' sake, here's a non-functional solution again.

```js
function showGuess(word, guesses) {
  let word_with_underscores = '';
  for (let i = 0; i < word.length; i++) {
    let letter = word[i];
    if (guesses.indexOf(letter) < 0) {
      word_with_underscores += '_ ';
    } else {
      word_with_underscores += letter + ' ';
    }
  }
  return word_with_underscores;
}
```
