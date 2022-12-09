# JS Copy an Object – How to Clone an Obj in JavaScript

A JavaScript object is a collection of key-value pairs. It is a non-primitive data type that can contain various data types. For example:

```javascript
const userDetails = {
  name: "John Doe",
  age: 14,
  verified: false
};
```

When working with objects in JavaScript, you may sometimes want to change the value or add a new property to the object.

In some scenarios, before you update or add new properties, you will want to create a new object and copy or clone the value of the original one.

For example, if you want to copy the value of the `userDetails` object and then change the name to something different. In the typical sense, you will want to use the equality (=) operator.

```javascript
const newUser = userDetails;
console.log(newUser); // {name: 'John Doe', age: 14, verified: false}
```

Everything still seems to be fine, but let's see what happens if we edit our second object:

```javascript
const newUser = userDetails;
newUser.name = "Jane Doe";

console.log(newUser); // {name: 'Jane Doe', age: 14, verified: false}
```

Everything is fine with the new object, but if you try to check your original object's values, you will notice it is affected. Why? How?

```javascript
console.log(userDetails); // {name: 'Jane Doe', age: 14, verified: false}
```

This is the issue. The original object is affected because objects are **reference types**. This means any value you store either in the clone or original object points to the same object.

This is not what you want. You want to store an object's value in a new object and manipulate the value in the new object without affecting the original array.

In this article, you will learn three methods that you can use to do this. You will also learn what deep and shallow clones mean and how they work.

In case you are in a rush, here are the three methods and an example of how they work.

```javascript
// Spread Method
let clone = { ...userDetails }

// Object.assign() Method
let clone = Object.assign({}, userDetails)

// JSON.parse() Method
let clone = JSON.parse(JSON.stringify(userDetails))
```

If you are not in a rush, let's get started.🚀

## How to Clone an Object in JavaScript With the Spread Operator

The spread operator was introduced in ES6 and can spread values into an object with the three dots in front.

```javascript
// Declaring Object
const userDetails = {
  name: "John Doe",
  age: 14,
  verified: false
};

// Cloning the Object with Spread Operator
let cloneUser = { ...userDetails };

console.log(cloneUser); // {name: 'John Doe', age: 14, verified: false}
```

This is no longer referenced, meaning changing the object's value will not affect the original object.

```javascript
// Cloning the Object with Spread Operator
let cloneUser = { ...userDetails };

// changing the value of cloneUser
cloneUser.name = "Jane Doe"

console.log(cloneUser.name); // 'Jane Doe'
console.log(cloneUser); // {name: 'Jane Doe', age: 14, verified: false}
```

When you check the name value in the original object or the entire object, you will notice it is not affected.

```javascript
console.log(userDetails.name); // 'John Doe'
console.log(userDetails); // {name: 'John Doe', age: 14, verified: false}
```

***Note***: You can only use the spread syntax to make a shallow copy of an object while deeper objects are referenced. You will understand when we get to the last section of this article.

## How to Clone an Object in JavaScript With `Object.assign()`

An alternative to the spread operator is the `Object.assign()` method. You use this method to copy the values and properties from one or more source objects to a target object.

```javascript
// Declaring Object
const userDetails = {
  name: "John Doe",
  age: 14,
  verified: false
};

// Cloning the Object with Object.assign() Method
let cloneUser = Object.assign({}, userDetails);

console.log(cloneUser); // {name: 'John Doe', age: 14, verified: false}
```

This is no longer referenced, meaning changing the object's value will not affect the original object.

```javascript
// Cloning the Object with Object.assign() Method
let cloneUser = Object.assign({}, userDetails);

// changing the value of cloneUser
cloneUser.name = "Jane Doe"

console.log(cloneUser.name); // 'Jane Doe'
console.log(cloneUser); // {name: 'Jane Doe', age: 14, verified: false}
```

When you check the name value in the original object or the entire object, you will notice it is not affected.

```javascript
console.log(userDetails.name); // 'John Doe'
console.log(userDetails); // {name: 'John Doe', age: 14, verified: false}
```

***Note***: You can only use the `Object.assign()` method to make a shallow copy of an object while deeper objects are referenced. You will understand when we get to the last section of this article.

## How to Clone an Object With `JSON.parse()`

The final method is `JSON.parse()`. You will use this method alongside `JSON.stringify()`. You can use this to deeply clone, but it has some downsides. First, let’s see how it works.

```javascript
// Declaring Object
const userDetails = {
  name: "John Doe",
  age: 14,
  verified: false
};

// Cloning the Object with JSON.parse() Method
let cloneUser = JSON.parse(JSON.stringify(userDetails));

console.log(cloneUser); // {name: 'John Doe', age: 14, verified: false}
```

Also, just like the previous methods, this is no longer referenced. This means that you can change a value in the new object without affecting the original object.

```javascript
// Cloning the Object with JSON.parse() Method
let cloneUser = JSON.parse(JSON.stringify(userDetails));

// changing the value of cloneUser
cloneUser.name = "Jane Doe"

console.log(cloneUser.name); // 'Jane Doe'
console.log(cloneUser); // {name: 'Jane Doe', age: 14, verified: false}
```

When you check the name value in the original object or the entire object, you will notice it is not affected.

```javascript
console.log(userDetails.name); // 'John Doe'
console.log(userDetails); // {name: 'John Doe', age: 14, verified: false}
```

***Note***: This method can be used for deep cloning but will not be the best option because it does not work with `function` or `symbol` properties.

Let’s now explore shallow and deep cloning and how you can use the `JSON.parse()` method to perform deep cloning. You will also learn why it is not the best option.

## Shallow Clone vs. Deep Clone

So far, the example used in this article is a basic object with only one level. This means that we have only performed shallow clone(s). But when an object has more than one level, then you will be required to perform a deep clone.

```javascript
// Shallow object
const userDetails = {
  name: "John Doe",
  age: 14,
  verified: false
};

// Deep object
const userDetails = {
  name: "John Doe",
  age: 14,
  status: {
    verified: false,
  }
};
```

Notice that the deep object has more than one level because there is another object in the `userDetails` object. A deep object can have as many levels as you want.

***Note***: When you use the spread operator or `Object.assign()` method to clone a deep object, the deeper objects will be referenced.

```javascript
const userDetails = {
  name: "John Doe",
  age: 14,
  status: {
    verified: false
  }
};

// Cloning the Object with Spread Operator
let cloneUser = { ...userDetails };

// Changing the value of cloneUser
cloneUser.status.verified = true;

console.log(cloneUser); // {name: 'John Doe', age: 14, status: {verified: true}}
console.log(userDetails); // {name: 'John Doe', age: 14, status: {verified: true}}
```

You will notice that both the original and new objects are affected because when you use either the spread operator or `Object.assign()` method to clone a deep object, the deeper objects will be referenced.

### How can you fix this issue

You can use the `JSON.parse()` method, and everything will work fine.

```javascript
const userDetails = {
  name: "John Doe",
  age: 14,
  status: {
    verified: false
  }
};

// Cloning the Object with Spread Operator
let cloneUser = JSON.parse(JSON.stringify(userDetails));

// Changing the value of cloneUser
cloneUser.status.verified = true;

console.log(cloneUser); // {name: 'John Doe', age: 14, status: {verified: true}}
console.log(userDetails); // {name: 'John Doe', age: 14, status: {verified: false}}
```

But there is an issue with this method. The issue is that you can lose your data. How?

`JSON.stringify()` works very well with primitive data types like numbers, strings, or Booleans, and that is what you have seen in our previous examples. But sometimes, `JSON.stringify()` is unpredictable if you are not aware of some values and how it handles them.

For example, it does not work with functions, symbols, or `undefined` values. It also changes other values like `NaN` and `Infinity` to `null`, breaking your code. When you have a function, symbol, or undefined value, it will return an empty key-value pair and skip it.

```javascript
const userDetails = {
  name: "John Doe",
  age: 14,
  status: {
    verified: false,
    method: Symbol(),
    title: undefined
  }
};

// Cloning the Object with Spread Operator
let cloneUser = JSON.parse(JSON.stringify(userDetails));
```

Everything seems to work fine, but for the new object, `JSON.stringify()` will return no key-value pair for the undefined and symbol values.

```javascript
console.log(cloneUser); 

// Output
{
  name: "John Doe",
  age: 14,
  status: {
    verified: false
  }
};
```

This means you need to be careful. The best option to implement deep cloning will be to use **Lodash**. You can then be sure that none of your data will be lost.

```javascript
const userDetails = {
  name: "John Doe",
  age: 14,
  status: {
    verified: false,
    method: Symbol(),
    title: undefined
  }
};

console.log(_.cloneDeep(userDetails));
```

## Wrapping Up!

This article has taught you how to clone an object in JavaScript using three major methods. You've seen how those methods work, and when to use each one. You also learned about deep cloning.

You can read this article to understand why `JSON.parse(JSON.stringify())` is a bad practice to clone an object in JavaScript.

Have fun coding!

Article archived from: [https://www.freecodecamp.org/news/clone-an-object-in-javascript/](https://www.freecodecamp.org/news/clone-an-object-in-javascript/)
