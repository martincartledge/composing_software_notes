##### Lenses

> composable pair of pure getter and setter functions which focus on a particular field inside an object

The `getter` takes a whole and returns the part of the object that the lens is focused on:

```js
// view = whole => part
```

The `setter` takes a whole, and a value to set the part to, and returns a new whole with the part updated. Unlike a function which simply sets a value into an object’s member field, Lens setters are pure functions:

```js
// set = whole => part => whole
```

To get or set each field individually, you might create three lenses. One for each axis. You could manually create getters which focus on each field:

```js
const getX = ([x]) => x;
const getY = ([x, y]) => y;
const getZ = ([x, y, z]) => z;

console.log(
  getZ([10, 10, 100]) // 100
);
```

Likewise, the corresponding setters might look like this:

```js
const setY = ([x, _, z]) => (y) => [x, y, z];

console.log(
  setY([10, 10, 10])(999) // [10, 999, 10]
);
```

Why lenses?

- Lenses allow you to abstract state shape behind getters and setters
- If you later need to change the state shape, you can do so in the lens, and none of the code that depends on the lens will need to change
- a small change in requirements should require only a small change in the system.

Lens laws

- `view(lens, set(lens, value, store)) ≡ value` — If you set a value into the store, and immediately view the value through the lens, you get the value that was set.
- `set(lens, b, set(lens, a, store)) ≡ set(lens, b, store)` — If you set a lens value to a and then immediately set the lens value to b, it’s the same as if you’d just set the value to b.
- `set(lens, view(lens, store), store) ≡ store` — If you get the lens value from the store,
  and then immediately set that value back into the store, the value is unchanged.

Build native lenses:

```js
// Pure functions to view and set which can be used with any lens:

const view = (lens, store) => lens.view(store);
const set = (lens, value, store) => lens.set(value, store);
// A function which takes a prop, and returns naive
// lens accessors for that prop.
const lensProp = (prop) => ({
  view: (store) => store[prop],
  // This is very naive, because it only works for objects:
  set: (value, store) => ({
    ...store,
    [prop]: value,
  }),
});
// An example store object. An object you access with a lens
// is often called the "store" object:
const fooStore = {
  a: "foo",
  b: "bar",
};

const aLens = lensProp("a");
const bLens = lensProp("b");

// Destructure the `a` and `b` props from the lens using
// the `view()` function.
const a = view(aLens, fooStore);
const b = view(bLens, fooStore);
console.log(a, b); //'foo''bar'
// Set a value into our store using the `aLens`:
const bazStore = set(aLens, "baz", fooStore);
// View the newly set value.
console.log(view(aLens, bazStore)); //'baz'
```

Over

The lens map operation is commonly called “over” in JavaScript libraries. We can create it like this:

```js
// over = (lens,f:a=>a,store) => store
const over = (lens, f, store) => set(lens, f(view(lens, store)), store);
const uppercase = (x) => x.toUpperCase();

console.log(
  over(aLens, uppercase, store) // { a: "FOO", b: "bar" }
);
```

Setters mirror the functor laws:

```js
// if you map the identity function over a lens
// the store is unchanged.
{
  const id = (x) => x;
  const lens = aLens;
  const a = over(lens, id, store);
  const b = store;
  console.log(a, b);
}
```

Now it’s easy to see that lenses under the over operation also obey the functor composition law:

```js
{
  // over(lens,f) afterover(lensg)
  // is the same as over(lens, compose(f, g))
  const lens = aLens;
  const store = { a: 20 };
  const g = (n) => n + 1;
  const f = (n) => n * 2;
  const a = compose(over(lens, f), over(lens, g));
  const b = over(lens, compose(f, g));
  console.log(
    a(store) // {a: 42} b(store) // {a: 42}
  );
}
```
