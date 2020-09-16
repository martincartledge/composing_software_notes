##### What is Functional Programming?

Functional Programming

> a programming paradigm where applications are composed using pure functions, avoiding shared mutable state and side-effects

Object Oriented

> data and behaviors are colocated

Procedural

> an imperative style grouping algorithms into procedures which tend to rely on shared mutable state

Function composition

> the process of combining two or more functions in order to produce a new function or perform some computation

Shared state

> any variable, object, or memory space that exists in a shared scope, or as the property of an object being passed between scopes

Trie

> effectively deep frozen — meaning that no property can change, regardless of the level of the property in the object hierarchy

Side effects

> A side effect is any application state change that is observable outside the called function other than its return value

- Modifying any external variable or object property (e.g., a global variable, or a variable in the parent function scope chain)
- Logging to the console
- Writing to the screen
- Writing to a file
- Writing to the network
- Triggering any external process
- Calling any other functions with side-effects

High order function

> any function which takes a function as an argument, returns a function, or both

- Abstract or isolate actions, effects, or async flow control using callback functions, promises, monads, etc.
- Create utilities which can act on a wide variety of data types
- Partially apply a function to its arguments or create a curried function for the purpose of reuse
  or function composition
- Take a list of functions and return some composition of those input functions

Functor - "Mappable"

> a data structure that can be mapped over

> In the case of Array.prototype.map(), the container is an array, but other data structures can be functors, too — as long as they supply the mapping API.

```js
const double = (n) => n.points * 2;

const doubleMap = (numbers) => numbers.map(double);

console.log(
  doubleMap([
    { name: "ball", points: 2 },
    { name: "coin", points: 3 },
    { name: "candy", points: 4 },
  ])
); //[4,6,8]
```

> “A list expressed over time is a stream.”

Imperative

> programs spend lines of code describing the specific steps used to achieve the desired results — the flow control: How to do things

- Imperative code frequently utilizes statements. A statement is a piece of code which performs some action. Examples of commonly used statements include for, if, switch, throw, etc.

```js
constdoubleMap = (numbers) => {
  const doubled = [];
  for (let i = 0; i < numbers.length; i++) {
    doubled.push(numbers[i] * 2);
  }
  return doubled;
};

console.log(doubleMap([2, 3, 4])); //[4,6,8]
```

Declarative

> programs abstract the flow control process (the how gets abstracted away), and instead spend lines of code describing the data flow: What to do

```js
const doubleMap = (numbers) => numbers.map((n) => n * 2);
console.log(doubleMap([2, 3, 4])); //[4,6,8]
```

- Declarative code relies more on expressions. An expression is a piece of code which evaluates to some value. Expressions are usually some combination of function calls, values, and operators which are evaluated to produce the resulting value.

- Pure functions over shared state and side effects
- Immutability over mutable data
- Function composition over imperative flow control
- Generic utilities that act on many data types over object methods that only operate on their
  colocated data
- Declarative over imperative code (what to do, rather than how to do it)
- Expressions over statements
