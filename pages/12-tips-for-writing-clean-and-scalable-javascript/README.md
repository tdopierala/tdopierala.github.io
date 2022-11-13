## 12 tips for writing clean and scalable JavaScript

**Scaling your web apps can be tricky. Follow these 12 simple tips to help you write cleaner, more efficient JavaScript.**

#### 1. Isolate your code

The most important thing I can recommend to keep a codebase clean and readable is having specific chunks of logic (usually functions) separated by topic. If you write a function, the function should default to having only one purpose and should not do multiple things at once.

Also, you should avoid causing side effects, meaning in most cases, you should not change anything that is declared outside your function. You receive data into functions with parameters; everything else should not be accessed. If you wish to get something out of the function, ***return*** new values.

#### 2. Modularization

Of course, you can group multiple functions into one module (and/or class, if you wish) if these functions are used in a similar way or do similar things. For example, if you have many different calculations to do, split them up into isolated steps (functions) that you can chain. However, these functions can all be declared in one file (module). Here is the example in JavaScript:

```javascript
function add(a, b) {
    return a + b   
}

function subtract(a, b) {
    return a - b   
}

module.exports = {
    add,
    subtract
}

const { add, subtract } = require('./calculations')

console.log(subtract(5, add(3, 2))
```

If you are writing frontend JavaScript, definitely make use of default exports for the most important items and named exports for secondary items.

#### 3. Prefer multiple parameters over single object parameters

When declaring a function, you should always prefer multiple parameters over one parameter that expects an object:

```javascript
// GOOD
function displayUser(firstName, lastName, age) {
    console.log(`This is ${firstName} ${lastName}. She is ${age} years old.`)
}

// BAD
function displayUser(user) {
    console.log(`This is ${user.firstName} ${user.lastName}. She is ${user.age} years old.`)
}
```

The reason behind this is that you know exactly what you need to pass to the function when you look at the first line of the function declaration.

Even though functions should be limited in size — doing only one job — it may happen that functions grow bigger in size. Scanning through the function body for the variables you need to pass (that are nested inside an object) will take you more time. Sometimes it might seem easier to just use the whole object and pass it to the function, but to scale your application, this setup will definitely help.

There is a certain point where declaring specific parameters does not make sense. For me, it is above four or five function parameters. If your function grows that big, you should pivot to use object parameters.

The main reason here is that parameters need to be passed in a specific order. If you have optional parameters, you need to   pass ***undefined*** or ***null***. With object parameters, you can simply pass the whole object, where order and ***undefined*** values do not matter.

#### 4. Destructuring

Destructuring is a nice tool that was introduced with ES6. It lets you grab specific fields from an object and assign it to a variable immediately. You can use this for any kind of object or module.

```javascript
// EXAMPLE FOR MODULES
const { add, subtract } = require('./calculations')
```

It does make sense to only import the functions you need to use in your file instead of the whole module, and then access the specific functions from it. Similarly, when you decide that you definitely need an object as function parameter, use destructuring as well. This will still give you the overview of what is needed inside the function:

```javascript
function logCountry({name, code, language, currency, population, continent}) {
    let msg = `The official language of ${name} `
    if(code) msg += `(${code}) `
    msg += `is ${language}. ${population} inhabitants pay in ${currency}.`
    if(contintent) msg += ` The country is located in ${continent}`
}

logCountry({
    name: 'Germany',
    code: 'DE',
    language 'german',
    currency: 'Euro',
    population: '82 Million',
})

logCountry({
    name: 'China',
    language 'mandarin',
    currency: 'Renminbi',
    population: '1.4 Billion',
    continent: 'Asia',
})
```

As you can see, I still know what I need to pass to the function — even if it is wrapped in an object. To solve the problem of knowing what is required, see the next tip!

(By the way, this also works for React functional components.)

#### 5. Use default values

Default values for destructuring or even basic function parameters are very useful. Firstly, they give you an example of what value you can pass to the function. Secondly, you can indicate which values are required and which are not. Using the previous example, the full setup for the function could look like this:

```javascript
function logCountry({
    name = 'United States', 
    code, 
    language = 'English', 
    currency = 'USD', 
    population = '327 Million', 
    continent,
}) {
    let msg = `The official language of ${name} `
    if(code) msg += `(${code}) `
    msg += `is ${language}. ${population} inhabitants pay in ${currency}.`
    if(contintent) msg += ` The country is located in ${continent}`
}

logCountry({
    name: 'Germany',
    code: 'DE',
    language 'german',
    currency: 'Euro',
    population: '82 Million',
})


logCountry({
    name: 'China',
    language 'mandarin',
    currency: 'Renminbi',
    population: '1.4 Billion',
    continent: 'Asia',
})
```

Obviously, sometimes you might not want to use default values and instead throw an error if you do not pass a value. Oftentimes, however, this is a handy trick.

#### 6. Data scarcity

The previous tips lead us to one conclusion: do not pass around data that you don’t need. Here, again, it might mean a bit more work when setting up your functions. In the long run, however, it will definitely give you a more readable codebase. It is invaluable to know exactly which values are used in a specific spot.

#### 7. Line and indentation limit

I have seen big files — very big files. In fact, over 3,000 lines of code. Finding chunks of logic is incredibly hard in these files.

Therefore, you should limit your file size to a certain number of lines. I tend to keep my files below 100 lines of code. Sometimes, it is hard to break up files, and they will grow to 200–300 lines and, in rare occasions, up to 400.

Above this threshold, the file gets too cluttered and hard to maintain. Feel free to create new modules and folders. Your project should look like a forest, consisting of trees (module sections) and branches (groups of modules and module files). Avoid trying to mimic the Alps, piling up code in confined areas.

Your actual files, in comparison, should look like the Shire, with some hills (small levels of indentation) here and there, but everything relatively flat. Try to keep the level of indentation below four.

Maybe it is helpful to enable eslint-rules for these tips!

#### 8. Use prettier

Working in a team requires a clear style guide and formatting. ESLint offers a huge ruleset that you can customize to your needs. There is also `eslint --fix`, which corrects some of the errors, but not all.

Instead, I recommend using [Prettier](https://prettier.io/) to format your code. That way, developers do not have to worry about code formatting, but simply writing high-quality code. The appearance will be consistent and the formatting automatic.

#### 9. Use meaningful variable names

Ideally, a variable should be named based on its content. Here are some guidelines that will help you declare meaningful variable names.

**Functions**

Functions usually perform some kind of action. To explain that, humans use verbs — convert or display, for example. It is a good idea to name your functions with a verb in the beginning, e.g., `convertCurrency` or `displayUserName`.

**Arrays**

These will usually hold a list of items; therefore, append an ***s*** to your variable name. For example:

```javascript
const students = ['Eddie', 'Julia', 'Nathan', 'Theresa']
```

**Booleans**

Simply start with ***is*** or ***has*** to be close to natural language. You would ask something like, “Is that person a teacher?” → “Yes” or “No.” Similarly:

```javascript
const isTeacher = true // OR false
```

**Array functions**

`forEach`, `map`, `reduce`, `filter`, etc. are great native JavaScript functions to handle arrays and perform some actions. I see a lot of people simply passing ***el*** or ***element*** as a parameter to the callback functions. While this is easy and quick, you should also name these according to their value. For example:

```javascript
const cities = ['Berlin', 'San Francisco', 'Tel Aviv', 'Seoul']
cities.forEach(function(city) {
...
})
```

**IDs**

Oftentimes, you have to keep track of the ids of specific datasets and objects. When ids are nested, simply leave it as id. Here, I like to map MongoDB ***_id*** to simply ***id*** before returning the object to the frontend. When extracting ids from an object, prepend the type of the object. For example:

```javascript
const studentId = student.id
// OR
const { id: studentId } = student // destructuring with renaming
```

An exception to that rule is MongoDB references in models. Here, simply name the field after the referenced model. This will keep things clear when populating references documents:

```javascript
const StudentSchema = new Schema({
    teacher: {
        type: Schema.Types.ObjectId,
        ref: 'Teacher',
        required: true,
    },
    name: String,
    ...
})
```

#### 10. Use async / await where possible

Callbacks are the worst when it comes to readability — especially when nested. Promises were a nice improvement, but async/await has the best readability, in my opinion. Even for beginners, or people coming from other languages, this will help a lot. However, make sure you understand the concept behind it and do not mindlessly use it everywhere.

#### 11. Module import order

As we saw in tips 1 and 2, keeping logic in the right place is key to maintainability. In the same way, how you import different modules can reduce confusion in your files. I follow a simple structure when importing different modules:

```javascript
// 3rd party packages
import React from 'react'
import styled from 'styled-components'

// Stores
import Store from '~/Store'

// reusable components
import Button from '~/components/Button'

// utility functions
import { add, subtract } from '~/utils/calculate'

// submodules
import Intro from './Intro'
import Selector from './Selector'
```

> I used a React component as an example here since there are more types of imports. You should be able to adapt that to your specific use case.

#### 12. Get rid of console

`console.log` is a nice way of debugging — very simple, quick, and does the job. Obviously, there are more sophisticated tools, but I think every developer still uses it. If you forget to clean up logs, your console will eventually end up a giant mess. Then there is logs that you actually want to keep in your codebase; for example, warning and errors.

To solve this issue, you can still use `console.log` for debugging reasons, but for lasting logs, use a library like loglevel or winston. Additionally, you can warn for console statements with ESLint. That way you can easily globally look for `console...` and remove these statements.


Article archived from: https://morioh.com/p/33c295451efc?f=5c21fb01c16e2556b555ab32
