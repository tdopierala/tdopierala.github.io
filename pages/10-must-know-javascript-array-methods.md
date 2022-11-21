# 10 Must-Know JavaScript Array Methods

Let's see what filter, forEach, some, every, includes, map, reduce, sort, find, and findIndex are and how you can use them.

**TABLE OF CONTENTS**

- [filter()](#1-filter)
- [forEach()](#2-foreach)
- [some()](3-some)
- [every()](4-every)
- [includes()](5-includes)
- [map()](6-map)
- [reduce()](7-reduce)
- [sort()](8-sort)
- [find()](9-find)
- [findIndex()](10-findindex)

## 1. filter()

`filter` is the method whenever you want to, well, filter out values. Only want positive values? Only looking for objects that have a certain property? `filter` is your way to go.

The following is the signature of the `filter` method:

```javascript
filter(function (element, index, array) {
  // element is the element within the array
  // index is the index of the element in the array
  // array is a reference to the array filter works on
}, thisOverride);
// thisOverride is a way to override the semantical this within the callback function.
// If you set it to another object, calling this.anyThing would access anyThing within that
// object, and not the actual array.
```

**Example Use Case**

Imagine that you have an online shop. And now you want to send a discount code to all customers that live in a certain area.

```javascript
const getElibigleCustomers(customers, zipCode) {
  return customers.filter(
    (customer) => customer.address.zipCode === zipCode
  );
}
```

`getElibigleCustomers` returns all customers that have an address stored with a zipCode, which is the same zipCode you look for. All other customers are filtered out of the array.

**Reimplementing filter**

If you want to understand `filter` even better, let's try to reimplement it.

```javascript
function filter(callbackFn) {
  const newArray = [];

  for (let i = 0; i < this.length; i++) {
    if (callbackFn(this[i], i, this)) {
      newArray.push(this[i]);
    }
  }

  return newArray;
}

Array.prototype.filter = filter;
```

**Attention**: Bear in mind that you should never replace a prototype method of a built-in type yourself. But this is just to show you how a possible implementation might look.

As you see, `filter` is nothing else than a loop that executes a callback function for each element. All elements the callback function returns false for, are filtered out.

## 2. forEach()

`forEach` is a functional way to loop over array elements and execute some logic for each element. The method itself doesn't return a new array.

The following is the signature of the `forEach` method:

```javascript
forEach(function (element, index, array) {
  // element is the element within the array
  // index is the index of the element in the array
  // array is a reference to the array forEach works on
}, thisOverride);
// thisOverride is a way to override the semantical this within the callback function.
// If you set it to another object, calling this.anyThing would access anyThing within that
// object, and not the actual array.
```

**Example Use Case**

Let's stay with the example of the online shop. Now, you want to print all names of the customers you previously filtered out.

```javascript
getElibigleCustomers(customers, '123456')
  .forEach(
    (customer) => console.log(`${customer.forename} ${customer.surname}`)
  );
```

When forEach executes, the console prints the full name of all customers that were previously filtered out.

**Reimplementing forEach**

Let's reimplement `forEach` so you better understand how it works.

```javascript
function forEach(callbackFn) {
  for (let i = 0; i < this.length; i++) {
    callbackFn(this[i], i, this);
  }
}

Array.prototype.forEach = forEach;
```

Once again, bear in mind that you should never replace prototype methods of built-in types in a real app, except you really know what you are doing.

You probably begin to notice a pattern by now. `forEach` is, once again, nothing else than a loop. And within this loop, the callback function is called. The result isn't interesting and thus thrown away.

## 3. some()

`some` is a special array method. It tests whether at least one element within the array tests positive for a specific condition. If so, `some` returns true, otherwise, it returns false.

The following is the signature of the some method:

```javascript
some(function (element, index, array) {
  // element is the element within the array
  // index is the index of the element in the array
  // array is a reference to the array some works on
}, thisOverride);
// thisOverride is a way to override the semantical this within the callback function.
// If you set it to another object, calling this.anyThing would access anyThing within that
// object, and not the actual array.
```

**Example Use Case**

Back to our online shop example. Imagine that you now want to test whether at least some of the customers you filtered out are underage. If so, you want to show them another deal, because everyone else gets a discount for alcoholic drinks. But you don't want to support underage children drinking, of course.

```javascript
const eligibleCustomers = getElibigleCustomers(customers, '123456')

const containsUnderAgedCustomers = eligibleCustomers.some(
  (customer) => customer.age < 18
);
```

When `some` executes, it checks each customer's age property. If at least one is below 18, it returns false.

**Reimplementing some**

Time to reimplement `some`.

```javascript
function some(callbackFn) {
  for (let i = 0; i < this.length; i++) {
    if (callbackFn(this[i], i, this)) {
      return true;
    }
  }
  return false;
}

Array.prototype.some = some;
```

`some` loops through all elements of the array until it finds an element where the callback function returns true for. In this case, the method returns early, because for some elements to satisfy a condition, one is already enough. Only when no element matches, false is returned.

## 4. every()

`every` is the counterpart of `some`. It tests whether all elements satisfy a condition. Only then, the method returns true. If only one element fails the test, false is returned.

The following is the signature of the `every` method:

```javascript
every(function (element, index, array) {
  // element is the element within the array
  // index is the index of the element in the array
  // array is a reference to the array every works on
}, thisOverride);
// thisOverride is a way to override the semantical this within the callback function.
// If you set it to another object, calling this.anyThing would access anyThing within that
// object, and not the actual array.
```

**Example Use Case**

Many customers who received your discount code have ordered by now. To save on shipment costs, you want to send it out all at once. But first, you need to check whether all those customers have valid address data saved.

```javascript
const customersWhoOrdered = getCustomersForOrder('discount1234');

const allCustomersHaveValidShipmentData = customersWhoOrdered
  .every(
    (customer) => hasValidShipmentData(customer)
  );
```

When `every` executes, it passes each customer to a function that checks whether that customer has valid shipment data stored. If only one customer has invalid data, the whole function returns false.

**Reimplementing every**

Time to reimplement `every`.

```javascript
function every(callbackFn) {
  for (let i = 0; i < this.length; i++) {
    if (!callbackFn(this[i], i, this)) {
      return false;
    }
  }
  return true;
}

Array.prototype.every = every;
```

`every` loops through all elements of the array until it finds an element where the callback function returns false for. In this case, the method returns early, because not **all** elements satisfy the condition. One is already enough. Only when no element matches, true is returned.

You might even have noticed that `every` is not very different from `some`. At some specific points, true is replaced with false, and the check with the callback function is negated. These small changes are already enough to make the method do exactly what you want.

## 5. includes()

`includes` is a method that checks whether an array contains a specific element. It's good for a quick check, but it also has its drawbacks, which we talk about in a minute.

The following is the signature of the `includes` method:

```javascript
includes(function (searchElement, fromIndex) {
  // searchElement is the element you look for
  // fromIndex is the index the search should start at
});
```

**Example Use Case**

`includes` is special. It actually tests for strict equality, which means: It either searches for a value that is strictly equal to the search element, or it looks for the exact reference of an object.

Let's say you want to check whether the customers orders include a very specific order, like this:

```javascript
const allOrders = getAllOrders();

const containsSpecificOrder = allOrders.includes({
  customer: 'John Doe'
  zipCode: '54321'
});
```

You would probably be surprised to find out that include returns false, even if the array contains an object with the exact same properties. This is because it looks for strict equality, and objects are only strictly equal if they are the same reference. JavaScript does not know an equals method.

This reduces `includes` use cases to primitive values. If you, for example want to check whether an array of numbers contains a specific number like this:

```javascript
const numbers = [1, 2, 3, 4, 5];

const includesFive = numbers.includes(5);
```

Here is a rule of thumb: If you deal with an array of primitive values, use `includes`. If you deal with objects, use `some` because it allows you to pass in a callback with which you can test objects for equality.

**Reimplementing includes**

Time to reimplement `includes`.

```javascript
function includes(searchElement, fromIndex = 0) {
  if (fromIndex > this.length || fromIndex < 0) {
    return false;
  }

  for (let i = fromIndex; i < this.length; i++) {
    if (this[i] === searchElement) {
      return true;
    }
  }

  return false;
}

Array.prototype.includes = includes;
```

The guard statements at the beginning are there to make the method execution a little safer. A negative fromIndex makes no sense, as well as an index larger than the array's max index. The rest is just a loop testing each element for strict equality with the element searched for.

## 6. map()

`map` is one of the most important array methods out there. Whenever you want to transform all values within an array, `map` is **the** way to go.

The following is the signature of the `map` method:

```javascript
map(function (element, index, array) {
  // element is the element within the array
  // index is the index of the element in the array
  // array is a reference to the array map works on
}, thisOverride);
// thisOverride is a way to override the semantical this within the callback function.
// If you set it to another object, calling this.anyThing would access anyThing within that
// object, and not the actual array.
```

**Example Use Case**

Let's jump back to the point where you had all eligible customers filtered. Now, you want to send their orders off and need to get all their addresses. This is a great use case for map:

```javascript
const eligibleCustomers = getElibigleCustomers(customers, '123456');

const addresses = eligibleCustomers
  .map((customer) => customer.address);
```

`map` iterates over all customers and then extracts all addresses. These are put into a new array and returned from the function.

**Reimplementing map**

Time to reimplement `map`.

```javascript
function map(callbackFn) {
  const newArray = [];
  for (let i = 0; i < this.length; i++) {
    const mappedValue = callbackFn(this[i], i, this);
    newArray.push(mappedValue);
  }
  return newArray;
}

Array.prototype.map = map;
```

`map` iterates over all elements of the array. For each element, it calls the callback function and expects a new value to be returned. This value is then pushed to a new array. That array is returned in full, resulting in an array of the same size as the original one, but with probably different elements in it.

## 7. reduce()

`reduce` is the most powerful array method existing. It can be used to reimplement all existing array methods, and it's the most flexible one. Talking about all the advantages it offers would definitely need an article on its own, but you will get a glimpse of it soon.

The following is the signature of the `reduce` method:

```javascript
reduce(function (accumulator, currentValue, currentIndex, array) {
  // accumulator is the result of the last call, or the initialValue in the beginning
  // currentValue is the value currently processed
  // currentIndex is the index of the current value within the array
  // array is a reference to the array reduce works on
}, initialValue);
```

**Example Use Case**

Remember when you wanted to find out whether there were underage customers? Another way to deal with this problem is to group all your eligible customers into two groups. Those of legal age, and those who are underage.

```javascript
const eligibleCustomers = getElibigleCustomers(customers, '123456');

const customerGroups = eligibleCustomers
  .reduce((accumulator, customer) => {
    if (customer.age > 18) {
      accumulator[0].push(customer);
    } else {
      accumulator[1].push(customer);
    }
    return accumulator;
  }, [[], []]);
```

`reduce` can be pretty difficult to understand but we can go over the above code together and see what it does. In this case, the accumulator is a 2-dimensional array. Index 0 contains all customers >= 18 years of age. Index 1 contains all customers who are underage. The first time reduce runs, it sets accumulator to the empty 2-dimensional array. Within the method, the code checks whether the age property of the customer is above 18. If so, it pushes the customer to the first array. If the customer is underaged, they get pushed to the second array. In the end, the 2-dimensional array with the grouped customers is returned.

**Reimplementing reduce**

Time to reimplement `reduce`.

```javascript
function reduce(callbackFn, initialValue) {
  let accumulator = initialValue ?? this[0];
  for (let i = 0; i < this.length; i++) {
    accumulator = callbackFn(accumulator, this[i], i, this);
  }
  return accumulator;
}

Array.prototype.reduce = reduce;
```

`reduce` iterates over all elements as all the other array methods do. In the beginning, the method needs to decide whether an initialValue was supplied. If not, the first element from the array is taken as such. After that, the accumulator is replaced with the result of calling the callback each time, and then returned in its final form in the end.

## 8. sort()

The name of `sort` already says it all. Whenever you want to sort an array, this is the method you need to call.

The following is the signature of the `sort` method:

```javascript
sort(function (firstElement, secondElement) {
  // firstElement is the first element to compare
  // secondElement is the second element to compare
});
```

**Example Use Case**

Whenever you need to sort something, you found a use case for `sort`. Let's, for example, try to sort your customers by age. For such a case, `sort` allows you to pass in a comparator function that you can use to tell `sort` how to properly order them.

```javascript
const customers = getCustomers();

customers.sort((a, b) => customer.a - customer.b);
```

The callback function must return a number based on the order of the elements. It should return a value < 0 if a comes before b, 0 if both are equal, and a value > 0 if a comes after b.

**Reimplementing sort**

Reimplementing `sort` is a little difficult because, under the hood, runtimes are allowed to implement any sorting algorithm they seem fitting. There are only a few requirements, like that the algorithm must be stable. Usually, runtimes implement at least QuickSort, though, and sometimes change the implementation based on the elements within the array.

```javascript
function partition(array, left, right, compareFunction) {
  let pivot = array[Math.floor((right + left) / 2)];
  let i = left;
  let j = right;
    while (i <= j) {
        while (compareFunction(array[i], pivot) < 0) {
            i++;
        }
        while (compareFunction(array[j], pivot) > 0) {
            j--;
        }
        if (i <= j) {
            [array[i], array[j]] = [array[j], array[i]]
            i++;
            j--;
        }
    }
    return i;
}

function quickSort(array, left, right, compareFunction) {
  let index;
  if (array.length > 1) {
      index = partition(array, left, right, compareFunction);
      if (left < index - 1) {
          quickSort(array, left, index - 1, compareFunction);
      }
      if (index < right) {
          quickSort(array, index, right, compareFunction);
      }
  }
  return array;
}

function sort(compareFunction) {
  return quickSort(this, 0, this.length - 1, compareFunction);
}

Array.prototype.sort = sort;
```

This is only an exemplary implementation of sort, in this case, QuickSort. But it should give you a general idea.

## 9. find()

`find` is your search function. Whenever you look for something within an array, you can use `find` to retrieve the first element from the array that satisfies your conditions.

The following is the signature of the `find` method:

```javascript
find(function (element, index, array) {
  // element is the current element
  // index is the current index
  // array is a reference to the array find works on
}, thisOverride);
// thisOverride is a way to override the semantical this within the callback function.
// If you set it to another object, calling this.anyThing would access anyThing within that
// object, and not the actual array.
```

**Example Use Case**

Imagine you try to find a customer with a specific name within all your customers.

```javascript
const customers = getCustomers();

const customerJohn = customers.find(
  (customer) => customer.forename === 'John'
);
```

In this case `find` returns the first user within the array that has the forename John. The important part is that `find` won't return all customers with that name.

**Reimplementing find**

Time to reimplement `find`.

```javascript
function find(callbackFn) {
  for (let i = 0; i < this.length; i++) {
    if (callbackFn(this[i], i, this)) {
      return this[i];
    }
  }
  return undefined;
}

Array.prototype.find = find;
```

`find` iterates over all elements as all the other array methods do. For every element, it checks whether the callback function returns true. If it does, it returns the element at that position. If it doesn't return early, it returns undefined at the end.

## 10. findIndex()

`findIndex` is a method that you can use to get the index of an element within the array. Like `find`, it stops at the first element that satisfies the condition. It will thus only ever return the index of the first element satisfying the test.

The following is the signature of the `findIndex` method:

```javascript
findIndex(function (element, index, array) {
  // element is the current element
  // index is the current index
  // array is a reference to the array find works on
}, thisOverride);
// thisOverride is a way to override the semantical this within the callback function.
// If you set it to another object, calling this.anyThing would access anyThing within that
// object, and not the actual array.
```

**Example Use Case**

Imagine you have all your customers sorted by age, and now you want to find the first customer with a forename of John.

```javascript
const customers = getCustomers();
const customersSortedByAge = sortByAge(customers);

const indexOfJohn customersSortedByAge.findIndex((customer) => customer.forename === 'John');
const customerJohn = customersSortedByAge[indexOfJohn];
```

In this case `findIndex` returns the index of the first user within the array that has the forename John. The important part is that `findIndex` won't return all indices of customers with that name.

**Reimplementing findIndex**

Time to reimplement `findIndex`.

```javascript
function findIndex(callbackFn) {
  for (let i = 0; i < this.length; i++) {
    if (callbackFn(this[i], i, this)) {
      return i;
    }
  }
  return -1;
}

Array.prototype.findIndex = findIndex;
```

`findIndex` iterates over all elements as all the other array methods do. You should notice the similarity to `find`. Instead of returning the element, only the index is returned when an element is found. Instead of undefined, if nothing is found, -1 is returned.

Article archived from: [https://morioh.com/p/e70e5ead0376](https://morioh.com/p/e70e5ead0376)
