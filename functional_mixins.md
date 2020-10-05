##### Functional Mixins

> composable factory functions which connect together in a pipeline; each function adding some properties or behaviors like workers on an assembly line

Features:

- Data privacy/encapsulation
- Inheriting private state
- Inheriting from multiple sources
- No diamond problem (property collision ambiguity) – last in wins
- No base-class requirement

The atomic units of composition are one of two things:

- Functions
- Data structures

Problems with class inheritance:

- _*The tight coupling problem*_: Because child classes are dependent on the implementation of the parent class, class inheritance is the tightest coupling available in object oriented design.
- _*The fragile base class problem*_: Due to tight coupling, changes to the base class can potentially
  break a large number of descendant classes — potentially in code managed by third parties. The
  author could break code they’re not aware of.
- _*The inflexible hierarchy problem*_: With single ancestor taxonomies, given enough time and
  evolution, all class taxonomies are eventually wrong for new use-cases.
- _*The duplication by necessity problem*_: Due to inflexible hierarchies, new use cases are often implemented by duplication, rather than extension, leading to similar classes which are unexpectedly divergent. Once duplication sets in, it’s not obvious which class new classes should descend from, or why.
- _*The gorilla/banana problem*_: “...the problem with object-oriented languages is they’ve got all this implicit environment that they carry around with them. You wanted a banana but what you got was a gorilla holding the banana and the entire jungle.” ∼ Joe Armstrong, “Coders at Work”

##### Mixins

> a form of object composition, where component features get mixed into a composite object so that properties of each mixin become properties of the composite object.

```js
const chocolate = { hasChocolate: () => true };
const caramelSwirl = { hasCaramelSwirl: () => true };
const pecans = { hasPecans: () => true };
const iceCream = Object.assign({}, chocolate, caramelSwirl, pecans);
/*
  // or,if your environment supports object spread... 
  const iceCream = {...chocolate, ...caramelSwirl, ...pecans}; 
*/
console.log(`
  hasChocolate: ${iceCream.hasChocolate()} 
  hasCaramelSwirl: ${iceCream.hasCaramelSwirl()} 
  hasPecans: ${iceCream.hasPecans()}
`);

/*
  hasChocolate: true
  hasCaramelSwirl: true
  hasPecans: true

*/
```

##### Functional Inheritance

> the process of inheriting features by applying an augmenting function to an object instance

- The function supplies a closure scope which you can use to keep some data private
- The augmenting function uses dynamic object extension to extend the object instance with new properties and methods

```js
function base(spec) {
  var that = {}; // Create an empty object
  that.name = spec.name; // Add it a "name" property return that;
  return that; // Return the object
}
//Construct a child object, inheriting from "base"
function child(spec) {
  var that = base(spec); // Create the object through the "base" constructor
  // Augment that object
  that.sayHello = function () {
    return "Hello, I'm " + that.name;
  };
  return that; // Return it
}
//Usage
var result = child({ name: "a functional object" });
console.log(result.sayHello()); // 'Hello, I'm a functional object'
```

##### Functional Mixin

> composable functions which mix new properties or behaviors into existing objects

```js
const flying = (o) => {
  let isFlying = false;
  return Object.assign({}, o, {
    fly() {
      isFlying = true;
      return this;
    },
    isFlying: () => isFlying,
    land() {
      isFlying = false;
      return this;
    },
  });
};
const bird = flying({});
console.log(bird.isFlying()); //false
console.log(bird.fly().isFlying()); //true
```

```js
const quacking = (quack) => (o) => Object.assign({}, o, { quack: () => quack });
const quacker = quacking("Quack!")({});
console.log(quacker.quack()); //'Quack!'
```

##### Composing functional mixins

```js
const createDuck = (quack) => quacking(quack)(flying({}));
const duck = createDuck("Quack!");
console.log(duck.fly().quack());
```

##### When to use functional mixins

- You should always use the simplest possible abstraction to solve the problem you’re working on.
- Start with a pure function.
- If you need an object with persistent state, try a factory function.
- If you need to build more complex objects, try functional mixins.

Use cases for functional mixins:

- Application state management, e.g., something similar to a Redux store.
- Certain cross-cutting concerns and services, e.g., a centralized logger.
- Composable functional data types, e.g., the JavaScript Array type implements Semigroup, Functor, Foldable... Some algebraic structures can be derived in terms of other algebraic structures, meaning that certain derivations can be composed into a new data type without customization.

##### Advice

- Favor pure functions > factories > functional mixins > classes
- Avoid the creation of is-a relationships between objects, mixins, or data types
- Avoid implicit dependencies between mixins – wherever possible, functional mixins should be
  self-contained, and have no knowledge of other mixins
  “Functional mixins” doesn’t mean “functional programming”
  There may be side-effects when you access a property using Object.assign() or object
  spread syntax ({...object}). You’ll also skip any non-enumerable properties. ES2017 added Object.getOwnPropertyDescriptors() to get around this problem.
