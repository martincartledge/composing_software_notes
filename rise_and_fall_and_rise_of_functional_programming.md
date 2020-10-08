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
