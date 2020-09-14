> “If I have seen further it is by standing on the shoulders of Giants.” ∼ Sir Isaac Newton

##### Composition

> “The act of combining parts or elements to form a whole.”

##### Software Development

> the act of breaking a complex problem down into smaller problems, and composing simple solutions to form a complete solution to the complex problem

##### Composing functions

_Function Composition_

> the process of applying a function to the output of another function

> If you’re chaining, you’re composing.

> Writing functions without mention of the arguments is called “point-free style”. To do it, you’ll call a function that returns the new function, rather than declaring the function explicitly.

> Less code = less surface area for bugs = fewer bugs.

_Composite Pattern_

> treat individual components and aggregated composites identically

Object Compositional Relationships:

- Delegation

> when an object delegates property access to another object, as used in the state, strategy, and visitor patterns

- Acquaintance

> When an object knows about another object by reference, usually passed as a parameter: a uses-a relationship, e.g, a network request handler might be passed a reference to a logger to log the request — the request handler uses a logger

- Aggregation

> When child objects form part of a parent object: a has-a relationship, e.g., DOM children are component elements in a DOM node — A DOM node has children

The most common form of object composition in JavaScript is known as _object concatenation_ (aka, concatenative inheritance: informally, “mixin composition”)

_Building composites with class inheritance_

```js
class Foo {
  constructor() {
    this.a = "a";
  }
}

class Bar extends Foo {
  constructor(options) {
    super(options);
    this.b = "b";
  }
}

const myBar = new Bar(); // {a: 'a', b: 'b'}
```

_Building composites with mixin composition_

```js
const a = {
  a: "a",
};

const b = {
  b: "b",
};

const c = { ...a, ...b }; // {a: 'a', b: 'b'}
```

> You want to select the simplest, most flexible solution for the task at hand.

##### The Dao of Immutability (The Way of the Functional Programmer)

> “Sometimes, the elegant implementation is just a function. Not a method. Not a class. Not a framework. Just a function.”

> “Is it not true that the word for ‘not functional’ is ‘dysfunctional’?”

- Immutability

> The true constant is change. Mutation hides change. Hidden change manifests chaos. Therefore, the wise embrace history.

- Separation

> Logic is thought. Effects are action. Therefore the wise think before acting, and act only when the thinking is done.

> Keep functions small. Do one thing at a time, and do it well.

- Composition

> Plan for composition. Write functions whose outputs will naturally work as inputs to many other functions. Keep function signatures as simple as possible.

- Flow

> A list expressed over time is a stream.

> Shared objects and data fixtures can cause functions to interfere with each other. Threads competing for the same resources can trip each other up. A program can be reasoned about and outcomes predicted only when data flows freely through pure functions.

##### The Rise and Fall and Rise of Functional Programming (Composable Software)

Lambda calculus

> is a universal model of computation based on function application

Three important points that make lambda calculus special:

- Functions are always anonymous. In JavaScript, the right side of const sum = (x, y) => x + y is the anonymous function expression (x, y) => x + y.

- Functions in lambda calculus are always unary, meaning they only accept a single parameter.

> The n-ary function (x, y) => x + y can be expressed as a unary function like: x => y => x + y. This transformation from an n-ary function to a series of unary functions is known as currying.

- Functions are first-class, meaning that functions can be used as inputs to other functions, and functions can return functions.

```js
const compose = (f, g) => (x) => f(g(x));

const double = (n) => n * 2;

const inc = (n) => n + 1;

const transform = compose(double, inc);

transform(3); //8
```

> Composition is a simple, elegant, and expressive way to clearly model the behavior of software. The process of composing small, deterministic functions to create larger software components and functionality produces software that is easier to organize, understand, debug, extend, test, and maintain.


##### Why Learn Functional Programming in JavaScript?

- First class functions

> The ability to use functions as data values: pass functions as arguments, return functions, and assign functions to variables and object properties


- Anonymous functions and lambda syntax

> x => x * 2 is a valid function expression in JavaScript. Concise lambdas make it easier to work with higher-order functions


- Closures

> the bundling of a function with its lexical environment. Closures are created at function creation time. When a function is defined inside another function, it has access to the variable bindings in the outer function, even after the outer function exits

> Mutation -  is a change to data structure that happens in-place.

```js
const foo = {
  bar: 'baz'
};

foo.bar = 'qux'; //mutation
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