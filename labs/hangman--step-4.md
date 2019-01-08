```js
// These lines are needed to be able to read user input from the console
const readline = require('readline')
const rl = readline.createInterface({input:process.stdin, output:process.stdout})

function next(word, guesses) {
  let numWrongGuesses = wrongGuessCount(word, guesses);
  console.log(`[${showGuess(word, guesses)}] wrong guesses: ${numWrongGuesses}`);

  if (numWrongGuesses === 6) {
    console.log("You've lost!");
  }
  else if (isWinner(word, guesses)) {
    console.log("You've won!");
  }
  else {
    rl.question('next letter? ', answer => {
      const letter = answer.trim()[0];
      console.log('guessing letter:', letter);
      // (actually, you'd need to validate this as well)
      next(word, guesses.concat([ letter ]));
    });
  }
}
```