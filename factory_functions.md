Factory Function

> any function which is not a class or constructor that returns a (presumably new) object

concise method syntax

```js
const userName = "echo";
const avatar = "echo.png";
const user = {
  userName,
  avatar,
  setUserName(userName) {
    this.userName = userName;
    return this;
  },
};
console.log(user.setUserName("Foo").userName); //"Foo"
```

> `this` refers to the object which the method is called on

> You can also apply a method to any other arbitrary object using the function prototype methods, .call(), .apply(), or .bind()

turn our user object into a createUser() factory:

```js
const createUser = ({ userName, avatar }) => ({
  userName,
  avatar,
  setUserName(userName) {
    this.userName = userName;
    return this;
  },
});

console.log(createUser({ userName: "echo", avatar: "echo.png" }));
/*
 {
  "avatar": "echo.png",
  "userName": "echo",
  "setUserName": [Function setUserName]
 }
 */
```

Computed Property Keys

We can compute the value of keys to assign to:

```js
const arrToObj = ([key, value]) => ({ [key]: value });
console.log(arrToObj(["foo", "bar"])); //{"foo":"bar"}
```

Tuple

> an array consisting of a key/value pair

Default Parameters

- Users are able to omit parameters with suitable defaults.
- The function is more self-documenting because default values supply examples of expected
  input.
- IDEs and static analysis tools can use default values to infer the type expected for the parameter. For example, a default value of 1 implies that the parameter can take a member of the Number type.

```js
const createUser = ({ userName = "Anonymous", avatar = "anon.png" } = {}) => ({
  userName,
  avatar,
});
console.log(
  // { userName: "echo", avatar: 'anon.png' }
  createUser({ userName: "echo" })
  // { userName: "Anonymous", avatar: 'anon.png' } createUser()
);
```

> The last = {} bit just before the parameter signature closes means that if nothing gets passed in for this parameter, we’re going to use an empty object as the default

> When you try to destructure values from the empty object, the default values for properties will get used automatically, because that’s what default values do: replace undefined with some predefined value

Type Inference

> the process of inferring types based on the context in which they are used

> Composition is more of a way of thinking than a particular technique in code
