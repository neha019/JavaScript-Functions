#Keyed Collections
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

## Advantages of Map over Object
- The keys of an Object are Strings or Symbols, where they can be of any value for a Map.
- You can get the size of a Map easily, while you have to manually keep track of size for an Object.
- The iteration of maps is in insertion order of the elements.

## 3 Important Analogies:
- Use maps over objects when keys are unknown until run time, and when all keys are the same type and all values are the same type.
- Use maps if there is a need to store primitive values as keys because object treats each key as a string whether it's a number value, boolean value or any other primitive value.
- Use objects when there is logic that operates on individual elements.



