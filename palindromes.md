To solve problems recursively, we have to try to define the problem in terms of **itself**. This often looks like working backwards: assume you have the solution to the problem, and use it as a tool to solve the problem.

What is a palindrome? Let's try to define it recursively, but in plain English:

> A word is a palindrome if its first and last letters are the same, and the letters in between also form a palindrome.

```js
function palindrome(word) {
    // A zero-length word is a palindrome
    if (word.length === 0) {
        return true
    }
    return word[0] === word[word.length - 1] && palindrome(word.slice(1, -1))
}
```

# Faster Palindromes
Since copying strings can incur a significant cost in the long run, we will solve implement a similar solution that does NOT use slice.

```js
function palindrome(word, at) {
    if (at > (word.length / 2)) {
        return true
    }
    return word[at] === word[word.length - (1 + at)] && palindrome(word, at + 1)
}
```
