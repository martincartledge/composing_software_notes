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
