> “If I have seen further it is by standing on the shoulders of Giants.” ∼ Sir Isaac Newton

##### Composition

> “The act of combining parts or elements to form a whole.”

##### Software Development

> the act of breaking a complex problem down into smaller problems, and composing simple solutions to form a complete solution to the complex problem

##### Composing functions;

_Function Composition_

> the process of applying a function to the output of another function

> If you’re chaining, you’re composing.

> Writing functions without mention of the arguments is called “point - free style”.To do it, you’ll call a function that returns the new function, rather than declaring the function explicitly.

> Less code = less surface area for bugs = fewer bugs.

_Composite Pattern_

    > treat individual components and aggregated composites identically;

Object Compositional Relationships:

- Delegation

  > when an object delegates property access to another object, as used in the state, strategy, and visitor patterns

  - Acquaintance

  > When an object knows about another object by reference, usually passed as a parameter: a uses - a relationship, e.g, a network request handler might be passed a reference to a logger to log the request — the request handler uses a logger

- Aggregation

> When child objects form part of a parent object: a has - a relationship, e.g., DOM children are component elements in a DOM node — A DOM node has children;

The most common form of object composition in JavaScript is known as _object concatenation_(aka, concatenative inheritance: informally, “mixin composition”);

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

> You want to select the simplest, most flexible solution for the task at hand.;
