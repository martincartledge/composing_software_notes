##### Curried Functions

> A curried function is a function that takes multiple arguments one at a time.

```js
// add = a => b => Number
const add = (a) => (b) => a + b;
```

> always return a unary function: a function which takes one argument

##### Closure

> a function bundled with its lexical scope

##### Fixed

> variables are assigned values in the closure’s bundled scope

##### Partial Application

> a function which has been applied to some, but not yet all of its arguments

> A function with some of its parameters fixed is said to be partially applied

##### Point-free style

> a style of programming where function definitions do not make reference to the function’s arguments

##### Compose

[Reduce Right](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/ReduceRight)

> applies a function against an accumulator and each value of the array (from right-to-left) to reduce it to a single value

```js
const compose = (...fns) => (x) => fns.reduceRight((y, f) => f(y), x);
```

```js
const g = (n) => n + 1;
const f = (n) => n * 2;

// replace x => f(g(x)) with compose(f,g)
const h = compose(f, g);

h(20); // => 42
```

##### Trace

```js
const trace = (label) => (value) => {
  console.log(`${label}: ${value}`);
  return value;
};
```

```js
const compose = (...fns) => (x) => fns.reduceRight((y, f) => f(y), x);

const g = (n) => n + 1;
const f = (n) => n * 2;

const h = compose(trace("after f"), f, trace("after g"), g);
h(20);

/*
after g:21 
after f:42
*/
```

##### Pipe

```js
const pipe = (...fns) => (x) => fns.reduce((y, f) => f(y), x);
```
