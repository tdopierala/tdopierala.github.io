# Convert Array to JSON Object in JavaScript

### What is JSON?

JSON means JavaScript Object Notation. JSON is an extremely lightweight data-interchange format for data exchange between server-side and client side which is quick and easy to parse and generate.

## 1. Convert Array to JSON Object JavaScript

You can use `JSON.stringify` to convert an array into a JSON formatted string in JavaScript.

Suppose there is an array such as `[6, 7, 8, 9]`. If you want to convert this array to JSON Object in javascript. Let’s see the example below.

```javascript
    var arr = [5, 6, 7, 8]; 
    var arrayToString = JSON.stringify(Object.assign({}, arr));  // convert array to string
    var stringToJsonObject = JSON.parse(arrayToString);  // convert string to json object
    
    console.log(stringToJsonObject);
 ```
 
 ```json
   {
       "0": 5,
       "1": 6,
       "2": 7,
       "2": 8
   }
```

1. `JSON.stringify()` and `Object.assign()` method convert array to JSON string.
2. `JSON.parse()` method convert string to JSON object in javascript.

## 2. Converting an Object to an Array

When converting an object to an array, we’ll use the `.entries()` method from the `Object` class. This will convert our object to an array of arrays. Each nested array is a two-value list where the first item is the key and the second item is the value.

```javascript
const obj = {"1":5,"2":7,"3":0,"4":0,"5":0,"6":0,"7":0,"8":0,"9":0,"10":0,"11":0,"12":0};
console.log(Object.entries(obj));
```

## 3. Convert two dimensional ( 2d ) arrays to JSON Object JavaScript

Suppose there is an array such as

```javascript
var arr = [
    ["Status", "Name", "Marks", "Position"], 
    ["active", "Akash", 10.0, "Web Developer"],
    ["active", "Vikash", 10.0, "Front-end-dev"],
    ["deactive", "Manish", 10.0, "designer"],
    ["active", "Kapil", 10.0, "JavaScript developer"],
    ["active", "Manoj", 10.0, "Angular developer"],
];
```

If you want to convert this array to JSON Object in javascript. Let’s see the example below:

```javascript
//array.
var arr = [
    ["Status", "Name", "Marks", "Position"], 
    ["active", "Akash", 10.0, "Web Developer"],
    ["active", "Vikash", 10.0, "Front-end-dev"],
    ["deactive", "Manish", 10.0, "designer"],
    ["active", "Kapil", 10.0, "JavaScript developer"],
    ["active", "Manoj", 10.0, "Angular developer"],
];
 
//javascript create JSON object from two dimensional Array
function arrayToJSONObject (arr){
    //header
    var keys = arr[0];
 
    //vacate keys from main array
    var newArr = arr.slice(1, arr.length);
 
    var formatted = [],
    data = newArr,
    cols = keys,
    l = cols.length;
    for (var i=0; i<data.length; i++) {
            var d = data[i],
                    o = {};
            for (var j=0; j<l; j++)
                    o[cols[j]] = d[j];
            formatted.push(o);
    }
    return formatted;
}
```

Article archived from: [https://morioh.com/p/9acdbd845f36](https://morioh.com/p/9acdbd845f36)
