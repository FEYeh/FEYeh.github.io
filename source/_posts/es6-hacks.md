
title: 7 Hacks for ES6 Developers
categories:
  - 前端
date: 2018-08-24 20:42:00
tags: 前端

---
7 Hacks for ES6 Developers

# Hack #1 — Swap variables
Using Array Destructuring to swap values

```js
let a = 'world', b = 'hello'
[a, b] = [b, a]
console.log(a) // -> hello
console.log(b) // -> world
// Yes, it's magic
```


# Hack #2 — Async/Await with Destructuring
Once again, Array Destructuring is great. Combined with async/await and promises to make a complex flow — simple.

```js
const [user, account] = await Promise.all([
  fetch('/user'),
  fetch('/account')
])
```

# Hack #3 — Debugging
For anyone who likes to debug using console.logs, here’s something awesome (and yes, I heard of console.table):

```js
const a = 5, b = 6, c = 7
console.log({ a, b, c })
// outputs this nice object:
// {
//    a: 5,
//    b: 6,
//    c: 7
// }
```

# Hack #4 — One liners
Syntax can be so much more compact for array operations

```js
// Find max value
const max = (arr) => Math.max(...arr);
max([123, 321, 32]) // outputs: 321
// Sum array
const sum = (arr) => arr.reduce((a, b) => (a + b), 0)
sum([1, 2, 3, 4]) // output: 10
```

# Hack #5 — Array concatenation
The spread operator can be used instead of concat:

```js
const one = ['a', 'b', 'c']
const two = ['d', 'e', 'f']
const three = ['g', 'h', 'i']
// Old way #1
const result = one.concat(two, three)
// Old way #2
const result = [].concat(one, two, three)
// New
const result = [...one, ...two, ...three]
```

# Hack #6 — Cloning
Clone arrays and objects with ease:

```js
const obj = { ...oldObj }
const arr = [ ...oldArr ]
Note: This creates a shallow clone.
```

# Hack #7 — Named parameters
Making function and function calls more readable with destructuring:

```js
const getStuffNotBad = (id, force, verbose) => {
  ...do stuff
}
const getStuffAwesome = ({ id, name, force, verbose }) => {
  ...do stuff
}
// Somewhere else in the codebase... WTF is true, true?
getStuffNotBad(150, true, true)
// Somewhere else in the codebase... I ❤ JS!!!
getStuffAwesome({ id: 150, force: true, verbose: true })
```