## Writing Clean Code in JavaScript

### 7 JavaScript clean coding tips every developer should know

Writing clean code improves the maintainability of the application and make developers productive. However, some developers are unaware of the language features available to further enhance the code.

In this article, I will discuss how we can utilize the features of JavaScript to write clean code.

#### 1. Use Object Destructuring

Object destructuring allows you to take specific fields from an object and assign them to a variable instantly. It reduces the number of code lines we need to extract the object properties and makes your code easier to understand.

Object destructuring saves a great deal of explicit variable declarations, and it is really useful in situations when:

- Using multiple properties from an object.
- Using the same property multiple times.
- Using a property that is deeply nested in an object.

```javascript
const employee = {name: ‘ANE01’, email: ‘Anna@example.com’, phone:’0112–345–6789'};
//with destucturing
const {name, email, phone} = employee;
//without destucturing
const name = employee.name;
const email = employee.email;
const phone = employee.phone;
```

The output of the two examples above (with and without destructuring) are identical. But, using object destructuring makes the code much simpler and easier to understand.

#### 2. Use Multiple Parameters Over Single Object Parameter

When declaring a function, we should always use multiple input parameters instead of single object inputs. This approach helps developers easily understand the minimum number of parameters that need to be passed by looking at the method signature.

> Also, it improves the application performance since there is no need to create object parameters or collect garbage.

```javascript
//recommended
function CustomerDetail (CustomerName, CustomerType, Order){    
  console.log('This is ${CustomerName} of ${CustomerType} and need ${Order}');
} 
//not-recommended
function CustomerDetail (User){    
  console.log('This is ${User.CustomerName} of ${User.CustomerType} and need ${User.Order}');
}
```

However, if the number of input parameters increase, you should switch back to using object parameters to avoid unnecessary code complexities.

> **Note**: If you use TypeScript and have number of parameters, its easier to define the interface of the parameters to benefit from type checking and auto-suggestions.
 
#### 3. Make Use of Arrow Functions

Arrow functions provide a concise way of writing JavaScript functions while resolving the problem of accessing ***this*** property inside callbacks.

If you are using arrow functions, curly braces, parenthesis, function, and return keywords become optional. Most importantly, your code becomes more understandable and clearer.

The below example shows a comparison between a single-line arrow function without parentheses and a regular function.

```javascript
// Arrow function
const myOrder = order => console.log(`Customer need ${order}`);
// Regular Function
function(order){
   console.log(`Customer need ${order}`);
}
```

Although arrow functions are much simpler, we must understand when and how to use them.

> For example, using arrow functions is not the best approach when working with object prototypes, classes, or object literals.

Also, arrow functions cannot be used as function constructors. You will receive an error if you use the new keyword to create a new object from an arrow function.

#### 4. Use Template Literals for String Concatenations

Template literals are literals delimited with backticks (\`\`). It provides an easy way to create multiline strings and perform string interpolation.

For example, we can define a placeholder in a string to get rid of all unnecessary concatenations.

```javascript
//before
var name = 'Peter';
var message = 'Hi'+ name + ',';
//after
var name = 'Peter';
var message = `Hi ${name},`;
```

#### 5. Spread Extension Operator

The spread extension operator (…) is another feature introduced with ES6. It is capable of expanding the literals like arrays into individual elements with a single line of code.

This operator is really useful when we need to put an array or object into a new array or object or to combine multiple parameters in the array.

The below code shows how to combine 2 arrays using the spread operator. As you can see, it makes the code clean and easy to understand since we don’t need to use loops or conditions.

```javascript
let x = [car, bus,van];
let y = [bike, truck, ..x, lorry]
console.log (y);
// bike, truck, car, bus, van, lorry
```

#### 6. Avoid Callbacks

Callbacks used to be the most popular way to express and handle asynchronous functions in JavaScript programs. However, if you are still using it, I hope you already know the pain of handling multiple nested callbacks.

For example, the following code contains 4 callback functions, and it will become even harder as the code start to grow.

```javascript
function1(function (err, data) { 
  ...  
  function2(user, function (err, data) {
    ...
     function3(profile, function (err, data) {
      ...
      function4(account, function (err, data) {
        ....
      }); 
    }); 
  });
});
```

As a solution, ES6 and ES7 introduced, Promises and Async/Await to handle asynchronous functions, and they are much easier to use and makes your code easily understandable to others.

But, if you use Promises or Async/Await, your code will be clean and much easy to understand.

```javascript
// Promises
function1() 
.then(function2) 
.then(function3) 
.then(function2) 
.catch((err) => console.error(err));
// Async/Await
async function myAsyncFunction() {  
try {    
  const data1= await function1();    
  const data2= await function2(data1);    
  const data3= await function3(data2);    
  return function4(data4);  
} 
catch (e) {    
  console.error(err);  
}}
```

#### 7. Use Shorthand Whenever Possible

When working with conditions, the shorthand method can save you a lot of time and space.

For example, if you write a condition to check empty, null and undefined conditions for a variable, you must write 2 conditions within the if statement.

```javascript
if (x !== “” && x !== null && x !== undefined) { ... }
```

However, if you are using the shorthand operator, you just need to write a single condition like below:

```javascript
if ( !!x ) { ... }
```

#### Final Thoughts

In this article, I discuss how we can utilize the features of JavaScript to write clean code.
