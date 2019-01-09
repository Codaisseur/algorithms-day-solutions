# American Grades 1
The function that we need to implement needs to map a range of numbers to a set of strings.

```js
function toAmericanGrade(grade) {
    if (grade >= 9) {
        return 'A'
    }
    if (grade >= 8) {
        return 'B'
    }
    if (grade >= 7) {
        return 'C'
    }
    if (grade >= 6) {
        return 'D'
    }
    return 'F'
}
```

# American Grades 2
Since we already wrote a function that maps a single number grade to an American grade letter, doing it for an array is a matter of mapping:

```js
// Must include the "toAmericanGrade" function as well.
function toAmericanGrades(grades) {
    return grades.map(toAmericanGrade)
}
```

# American Grades 3
We've seen how to use `reduce` to calculate a sum. Since the average is the sum divided by the number of items, we can do the following:

```js
function averageAmericanGrade(grades) {
    return toAmericanGrade(grades.reduce((sum, value) => sum + value, 0) / grades.length)
}
```

A slightly different solution is to divide each value before summing it up. Due to the precision of numbers in JavaScript, this second solution may be less precise:

```js
function averageAmericanGrade(grades) {
    return toAmericanGrade(grades.reduce((sum, value) => sum + (value / grades.length), 0))
}
```