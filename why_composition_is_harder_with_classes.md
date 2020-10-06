##### The `new` keyword

What does `new` do?

- Creates a new object and binds this to it in the constructor function.
- Implicitly returns this, unless you explicitly return another object.
- Sets the instance [[Prototype]], instance.**proto** to Constructor.prototype, so that
  Object.getPrototypeOf(instance) === Constructor.prototype and instance.**proto**-
  === Constructor.prototype.
- Sets the instance.constructor === Constructor.

Prototype Delegation

> a convenient way to conserve memory if you have millions of objects, or to squeeze a micro-performance boost out of your program if you need to access tens of thousands of properties on an object within a 16 ms render loop cycle.

- The `[[Prototype]]` link is used for prototype delegation

In ES5, the Constructor.prototype link was dynamic and reconfigurable, which could be a handy feature if you need to create an abstract factory — but if you reassign the prototype, instanceof will give you false negatives if the Constructor.prototype does not currently reference the same object in memory that the instance `[[Prototype]]` references:

```js
class User {
  constructor({ userName, avatar }) {
    this.userName = userName;
    this.avatar = avatar;
  }
}

const currentUser = new User({ userName: "Foo", avatar: "foo.png" });

User.prototype = {};
console.log(
  currentUser instanceof User // <-- false -- Oops!
  // But it clearly has the correct shape:
  // { avatar: "foo.png", userName: "Foo" } currentUser
);
```

Multiple execution contexts ("realms")

> memory sandboxes where the same code will access different physical memory locations

> Object values in JavaScript are memory references under the hood, and different frames point to different locations in memory, so === checks will fail

The `constructor` property

> The `.of()` method is a factory that returns a new instance of the data type containing whatever you pass into `.of()`.

```js
const empty = ({ constructor } = {}) =>
  constructor.of ? constructor.of() : undefined;

const foo = [23];

console.log(
  empty(foo) // []
);
```

It’s easy to add support for .constructor and .of() to a factory:

```js
const createUser = ({ userName = "Anonymous", avatar = "anon.png" } = {}) => ({
  userName,
  avatar,
  constructor: createUser,
});

createUser.of = createUser;

//testing .of and .constructor:

const empty = ({ constructor } = {}) =>
  constructor.of ? constructor.of() : undefined;

const foo = createUser({ userName: "Empty", avatar: "me.png" });

console.log(
  empty(foo), // { avatar: "anon.png", userName: "Anonymous" }
  foo.constructor === createUser.of, // true
  createUser.of === createUser // true
);
```

You can even make .constructor non-enumerable by adding to the delegate prototype:

```js
const createUser = ({ userName = "Anonymous", avatar = "anon.png" } = {}) => ({
  __proto__: {
    constructor: createUser,
  },
  userName,
  avatar,
});
```

Factories allow increased flexibility because they:

- Decouple instantiation details from calling code.
- Allow you to return arbitrary objects — for instance, to use an object pool to tame the garbage
  collector.
- Don’t pretend to provide any type guarantees, so callers are less tempted to use instanceof and
  other unreliable type checking measures, which might break code across execution contexts,
  or if you switch to an abstract factory.
- Can dynamically swap implementations for abstract factories. e.g., a media player that swaps
  out the .play() method for different media types.
- Adding capability with composition is easier with factories.

> Our APIs should be open to extension, but closed to breaking changes.

> If your class API is public, or if you work on a very large app with a very large team, the refactor is likely to break code you’re not even aware of. It’s a better idea to deprecate the class entirely and replace it with a factory function to move forward.

`class` offers two kinds of performance optimizations: shared memory for properties stored on the delegate prototype, and property lookup optimizations.

Don’t micro-optimize for performance unless you’ve noticed a performance problem, profiled your application code, and pinpointed a real bottleneck.

It’s OK to use class if:

- You’re building UI components for a framework like React or Angular. Both frameworks wrap your component classes into factories and manage instantiation for you, so you don’t have to use new in your own code.
- You never inherit from your own classes or components. Instead, try object composition, function composition, higher order functions, higher order components, or modules — all of them are better code reuse patterns than class inheritance.
- You need to optimize performance. Just remember to export a factory so callers don’t have to use new and don’t get lured into the extends trap.
