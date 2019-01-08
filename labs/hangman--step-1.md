The one-liner solution for this problem would be the following:

```js
function wrongGuessCount(word, guesses) {
  return guesses
    .filter(letter => word.indexOf(letter) < 0)
    .length;
}
```

You should strive to be able to come up with a solution like this. In words, it reads: *"Select, out of the list of guesses, only those letters that don't occur in the word at all, then count them."*

If you would write it out in non-functional style, it would be:

```js
function wrongGuessCount(word, guesses) {
  let numWrong = 0;
  for (let i = 0; i < guesses.length; i++) {
    if (word.indexOf(guesses[i]) < 0) {
      numWrong++;
    }
  }
  return numWrong;
}
```

Although this solution is correct, it is not preferred, because it's less readable. (You have to "play computer" in your head to figure out what the loop is supposed to do. Luckily the variable `numWrong` was named reasonably, which helps you do this.)
