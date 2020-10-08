##### Why Learn Functional Programming in JavaScript?

- First class functions

> The ability to use functions as data values: pass functions as arguments, return functions, and assign functions to variables and object properties

- Anonymous functions and lambda syntax

> x => x \* 2 is a valid function expression in JavaScript. Concise lambdas make it easier to work with higher-order functions

- Closures

> the bundling of a function with its lexical environment. Closures are created at function creation time. When a function is defined inside another function, it has access to the variable bindings in the outer function, even after the outer function exits

> Mutation - is a change to data structure that happens in-place.

```js
const foo = {
  bar: "baz",
};

foo.bar = "qux"; //mutation
```

Here are some features that some functional languages have, that JavaScript does not have:

- Purity

> In some FP languages, purity is enforced by the language. Expressions with side-effects are not allowed.

- Immutability

> Some FP languages disable mutations. Instead of mutating an existing data structure, such as an array or object, expressions evaluate to new data structures. This may sound inefficient, but most functional languages use trie data structures under the hood, which feature structural sharing: meaning that the old object and new object share references to the data that is the same.

- Recursion

> Recursion is the ability for a function to reference itself for the purpose of iteration. In many FP languages, recursion is the only way to iterate. There are no loop statements like for, while, or do loops.

- Proper tail calls

> A language feature which allows recursive functions to reuse stack frames for recursive calls. Without proper tail calls, a call stack can grow without bounds and cause a stack overflow.

- Monad

> a data type that maps and flattens in one operation

> Apps ate the world, the web ate apps, and JavaScript ate the web.
