# Keyed Collections
The collection of data indexed by key such as using Map and Set objects which are iterable.

## Maps
A simple key/value map and can iterate its elements in insertion order.

``` javascript
//Map example 
var map = new Map();
map.set('name', 'Neha');
map.set('city','xyz');
map.size;
map.get('name');
map.has('city');
map.delete('pincode');

// clear all the key value pairs
map.clear();
map.size;

//returns a new Iterator object that contains the [key, value] pairs for each element in the Map object in insertion order.
var entry = map.entries();
entry.next().value;
entry.next().value;

//returns a new Iterator object that contains the keys for each element in the Map object in insertion order.
var key = map.keys();
key.next().value;

//returns a new Iterator object that contains the values for each element in the Map object in insertion order.
var val = map.values();
val.next().value;
```

### Advantages of Map over Object
- The keys of an Object are Strings or Symbols, where they can be of any value for a Map.
- You can get the size of a Map easily, while you have to manually keep track of size for an Object.
- The iteration of maps is in insertion order of the elements.

### 3 Important Analogies:
- Use maps over objects when keys are unknown until run time, and when all keys are the same type and all values are the same type.
- Use maps if there is a need to store primitive values as keys because object treats each key as a string whether it's a number value, boolean value or any other primitive value.
- Use objects when there is logic that operates on individual elements.

### WeakMap Objects
- The WeakMap object is a collection of key/value pairs in which the keys are objects only and the values can be arbitrary values. 
- WekaMap objects are weakly held
- A part of Garbage Collection if there is no other reference to the object anymore. 
- WeakMap keys are not enumerable

## Sets
As the name suggests, its a collection of values which are uniquesly held, may only occur once.

```javascript
var set = new Set();
set.add('some text');
set.add('foo');
set.add(1);
set.has(1);
set.delete('foo');
set.size();

set.clear();
set.size();

// returns a new Iterator object that contains an array of [value, value] for each element in the Set object, in insertion order.
var entry = set.entries();
for (const entry of iterator1) {
  console.log(entry);
}

function logSetElements(value1, value2, set) {
  console.log(`s[${value1}] = ${value2}`);
}

new Set(['foo', 'bar', undefined]).forEach(logSetElements);

const set1 = new Set();
set1.add(42);
set1.add('forty two');

const iterator1 = set1.values();
console.log(iterator1.next().value);
console.log(iterator1.next().value);

// The initial value of the @@iterator property is the same function object as the initial value of the values property.
const set1 = new Set();
set1.add(42);
set1.add('forty two');

const iterator1 = set1[Symbol.iterator]();
console.log(iterator1.next().value);
console.log(iterator1.next().value);
```

### Advantages of Set over Array
- Deleting Array elements by value (arr.splice(arr.indexOf(val), 1)) is very slow.
- Set objects let you delete elements by their value. With an array, you would have to splice based on an element's index.
- The value NaN cannot be found with indexOf in an array.
- Set objects store unique values. You don't have to manually keep track of duplicates.

### WeakSet Objects
- WeakSet objects are collections of objects only and not of arbitrary values of any type..
- WeakSet objects are not enumerable


