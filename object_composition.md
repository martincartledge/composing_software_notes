There are two important parts of abstraction:

- Generalization The process of extracting only the shared properties and behaviors that serve the general use case
- Specialization The process of providing the implementation details required to serve the special case

> Some good alternatives to class inheritance include simple functions, higher order functions, modules, and object composition.

> The act of constructing a composite type is known as composition.

> favor object composition over class inheritance

> Tightly coupled objects: monolithic systems, where you can’t change or remove a class without understanding and changing many other classes. The system becomes a dense mass that’s hard to learn, port, and maintain.

> encapsulation: functions outside the object can’t directly observe or manipulate the object’s private state

> message passing: the mechinism we use to communicate with objects - method calls are the simplest form

Three Different Forms of Object Composition

- Aggregation: When an object is formed from an enumerable collection of subobjects. In other words, an object which contains other objects. Each subobject retains its own reference identity, such that it could be destructured from the aggregation without information loss.
- Concatenation: When an object is formed by adding new properties to an existing object.Prop- erties can be concatenated one at a time or copied from existing objects, e.g., jQuery plugins are created by concatenating new methods to the jQuery delegate prototype, jQuery.fn.
- Delegation: When an object forwards or delegates to another object. e.g., Ivan Sutherland’s Sketchpad50 (1962) included instances with references to “masters” which were delegated to for shared properties. Photoshop includes “smart objects” that serve as local proxies which delegate to an external resource. JavaScript’s prototypes are also delegates: Array instances forward built-in array method calls to Array.prototype, objects to Object.prototype, etc...

> Reduce is a higher order function which takes a function and applies it over a collection of items.

> With each iteration, the new current value gets folded into the accumulator, where “fold” is not a single, well defined operation, but the operation suplied by the reducer function body.

And a basic object composition example, using concatenation via object spread syntax:

```js
const assign = (a, c) => ({ ...a, ...c });

const composed = [{ a: "a" }, { b: "b" }].reduce(assign, {});
// => { a: 'a',b: 'b'}
```

Aggregation

> An aggregate is an object which contains other objects.

> Each subobject in an aggregation retains its own reference identity, and could be losslessly destructured from the aggregate

Examples:

- Arrays
- Maps
- Sets
- Graphs
- Trees
  - DOM nodes (a DOM node may contain child nodes)
  - UI components (a component may contain child components)

Array aggregation:

```js
const collection = (a, e) => a.concat([e]);
const a = objs.reduce(collection, []);

console.log(
  "collection aggregation",
  a,
  a[1].b,
  a[2].c,
  `enumerable keys: ${Object.keys(a)}`
);

/*
  collection aggregation
  [{"a":"a","b":"ab"},{"b":"b"},{"c":"c","b":"cb"}]
  bc
  enumerable keys: 0,1,2
*/
```

Linked list aggregation using pairs:

```js
const pair = (a, b) => [b, a];
const l = objs.reduceRight(pair, []);

console.log("linked list aggregation", l, `enumerable keys: ${Object.keys(l)}`);

/* 
  linked list aggregation 
  [
    {"a":"a","b":"ab"}, [
      {"b":"b"}, [
        {"c":"c","b":"cb"},
        []
      ]
    ]
  ]

  enumerable keys: 0,1 
*/
```

> Linked lists form the basis of lots of other data structures and aggregations, such as arrays, strings, and various kinds of trees. The DOM tree is based on linked lists, with DOM nodes pointing to children, children nodes pointing back to parents, and delegated references to sibling nodes

Concatenation

> when an object is formed by adding new properties to an existing object

Examples:

- State reducers (e.g., Redux)
- Functional mixins

When to use:

- merging JSON objects
- hydrating application state from multiple sources
- creating updates to immutable state (by merging previous state with new data)

```js
const concatenate = (a, o) => ({ ...a, ...o });
const c = objs.reduce(concatenate, {});
console.log("concatenation", c, `enumerable keys: ${Object.keys(c)}`);
// concatenation {a:'a',b:'cb',c:'c'} enumerable keys: a,b,c
```

Delegation

> when an object forwards or delegates to another object

Examples:

- JavaScript’s built-in types use delegation to forward built-in method calls up the prototype chain. e.g., [].map() delegates to Array.prototype.map(), obj.hasOwnProperty() delegates to Object.prototype.hasOwnProperty() and so on.
- Sketchpad’s “masters” were dynamic delegates. Modifications to the delegate would be reflected instantly in all of the object instances.
- Photoshop uses delegates called “smart objects” to refer to images and resources defined in separate files. Changes to the object that smart objects refer to are reflected in all instances of the smart object.

When to use:

- Conserve memory: Any time there may be potentially many instances of an object and it would be useful to share identical properties or methods among each instance which would otherwise require allocating more memory.
- Dynamically update many instances: Any time many instances of an object need to share identical state which may need to be updated dynamically and changes instantaneously reflected in every instance, e.g., Sketchpad’s “masters” or Photoshop’s “smart objects”.

```js
const delegate = (a, b) => Object.assign(Object.create(a), b);
const d = objs.reduceRight(delegate, {});
console.log("delegation", d, `enumerable keys: ${Object.keys(d)}`);

/*
  delegation {a:'a',b:'ab'}
  enumerable keys: a,b
*/

console.log(d.b, d.c); //abc
```
