# How to convert all Array values to LowerCase, UpperCase in JavaScript

You can also now achieve this very simply by using an arrow function and the `map()` method of the Array:

```javascript
var words = ['Foo','Bar','Fizz','Buzz'].map(v => v.toLowerCase());
console.log(words);
```

```javascript
var words = ['Foo','Bar','Fizz','Buzz'].map(v => v.toUpperCase());
console.log(words);
```

Note that `map()` will only work in browsers which support **ES2015**. In other words, anything except IE8 and lower.

Similarly, arrow functions will not work at all in IE. For a legacy browser safe version you would need to use an anonymous function:

```javascript
var words = ['Foo','Bar','Fizz','Buzz'].map(function(v) {
  return v.toLowerCase();
});
console.log(words);
```

```javascript
var words = ['Foo','Bar','Fizz','Buzz'].map(function(v) {
  return v.toUpperCase();
});
console.log(words);
```

With arrays, the `+=` operator does not do what you expect - it calls `.toString` on the array and concatenates them. Instead, you want to use the array push method:

```javascript
var sorted = [];
for (var i = 0; i < words.length; i++) {
    sorted.push(words[i].toLowerCase());
}
console.log(sorted);
```

```javascript
var sorted = [];
for (var i = 0; i < words.length; i++) {
    sorted.push(words[i].toUpperCase());
}
console.log(sorted);
```

If you want fast and have a very large array of words

```javascript
sorted=words.join('|').toLowerCase().split('|');
```

```javascript
sorted=words.join('|').toUpperCase().split('|');
```

Article archived from: [https://morioh.com/p/0b5bd0ececd4](https://morioh.com/p/0b5bd0ececd4)
