# Merge two JSON objects with same key in JavaScript

Using Nested for loop you can Merge two JSON objects with the same key JavaScript.

### Merge two JSON objects with same key JavaScript

Simple example code.

```javascript
var g = [
  { id: 36, name: 'AAA', goal: 'yes' },
  { id: 40, name: 'BBB', goal: 'yes' },
  { id: 57, name: 'CCC', goal: 'yes' },
  { id: 14, name: 'DDD', goal: 'yes' },
  { id: 39, name: 'EEE', goal: 'yes' },
  { id: 37, name: 'FFF', goal: 'yes' },
  { id: 59, name: 'GGG', goal: 'yes' },
  { id: 50, name: 'III', goal: 'yes' },
  { id: 43, name: 'HHH', goal: 'yes' },
  { id: 35, name: 'JJJ', goal: 'yes' }
],
 
c = [
  { id: 36, name: 'AAA', circle: 'yes' },
  { id: 40, name: 'BBB', circle: 'yes' },
  { id: 57, name: 'CCC', circle: 'yes' },
  { id: 42, name: 'ZZZ', circle: 'yes' },
  { id: 14, name: 'DDD', circle: 'yes' },
  { id: 39, name: 'EEE', circle: 'yes' },
  { id: 37, name: 'FFF', circle: 'yes' },
  { id: 59, name: 'GGG', circle: 'yes' },
  { id: 43, name: 'HHH', circle: 'yes' },
  { id: 35, name: 'JJJ', circle: 'yes' },
  { id: 100, name: 'JJJ', circle: 'yes' }
],
 
arrayList = [], obj_c_processed = [];

for (var i in g) {
  var obj = {id: g[i].id, name: g[i].name, goal: g[i].goal};

  for (var j in c) {
    if (g[i].id == c[j].id) {
      obj.circle = c[j].circle;
      obj_c_processed[c[j].id] = true;
    }
  }

  obj.circle = obj.circle || 'no';
  arrayList.push(obj);
}

for (var j in c){
  if (typeof obj_c_processed[c[j].id] == 'undefined') {
    arrayList.push({id: c[j].id, name: c[j].name, goal: 'no', circle: c[j].circle});
  }
}

console.log(arrayList);
```

Output:

![Console output](/images/merge-two-json-objects-with-same-key-in-js-img01.png)

**More example**

You could use `Map` and `Object.assign` for merging the objects.

```javascript
var request1 = [{
  ObjId: 174864,
  ObjMutationD: "2010-07-09T00:00:00.000Z",
  ObjMitarbeiterS: "epf",
  ObjAufId: 142
}, {
  ObjId: 175999,
  ObjMutationD: "2010-07-09T00:00:00.000Z",
  ObjMitarbeiterS: "epf",
  ObjAufId: 149
}],
request2 = [{
  ObjId: 174864,
  MulPfadS: "M:\\Originalbilder\\FGS\\95nn",
  MulDateiS: "9576.305-034-1",
  MulExtentS: "jpg"
}, {
  ObjId: 177791,
  MulPfadS: "M:\\Originalbilder\\FGS\\95nn",
  MulDateiS: "9576.305-035-1",
  MulExtentS: "jpg"
}];

var result = [...[request1, request2].reduce((m, a) => (a.forEach(o => m.has(o.ObjId) && Object.assign(m.get(o.ObjId), o) || m.set(o.ObjId, o)), m), new Map).values()];

console.log(result);
```

### Use concat() for arrays

Assuming that you would like to merge two JSON arrays like the below:

```javascript
var json1 = [{id:1, name: 'xxx' ...}]
var json2 = [{id:2, name: 'xyz' ...}]
```

The solution is simply to use a JavaScript array `concat()`

```javascript
var finalObj = json1.concat(json2);
```

Article archived from: [https://tutorial.eyehunts.com/js/merge-two-json-objects-with-same-key-javascript-example-code/](https://tutorial.eyehunts.com/js/merge-two-json-objects-with-same-key-javascript-example-code/)
