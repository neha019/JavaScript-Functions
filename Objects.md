# Objects
In JavaScript, an object is a standalone entity, with properties and type. It is a collection of properties (key - value pair).

## Objects/Properties
- JavaScript object has properties associated with it.
- You access the properties of an object with a simple dot-notation:
``` javascript
objectName.propertyName

var myCar = new Object();
myCar.make = 'Ford';
myCar.model = 'Mustang';
myCar.year = 1969;
``` 
- Properties of JavaScript objects can also be accessed or set using a bracket notation
``` javascript
myCar['make'] = 'Ford';
myCar['model'] = 'Mustang';
myCar['year'] = 1969;
``` 
- All keys in the square bracket notation are converted to string unless they're Symbols.
- JavaScript object property names (keys) can only be strings or Symbols.
``` javascript
var propertyName = 'make';
myCar[propertyName] = 'Ford';

propertyName = 'model';
myCar[propertyName] = 'Mustang';
``` 

## Creating New Objects
Two ways:
- object initializers / literals
- _new_ operator
- Object.create() - rarely used
``` javascript
var Animal = {
  type: 'Invertebrates', 
  displayType: function() {  
    console.log(this.type);
  }
};

// Create new animal type called animal1 
var animal1 = Object.create(Animal);
animal1.displayType(); 

// Create new animal type called Fishes
var fish = Object.create(Animal);
fish.type = 'Fishes';
fish.displayType();
``` 

## Defining Getter Setter
- defined using object initializers, or
- added later to any object at any time using a getter or setter adding method.
``` javascript
var o = {
  a: 7,
  get b() { 
    return this.a + 1;
  },
  set c(x) {
    this.a = x / 2;
  }
};

console.log(o.a); 
console.log(o.b); 
o.c = 50;         
console.log(o.a);
```
- Getters and setters can also be added using the Object.defineProperties method. 
``` javascript
var o = { a: 0 };

Object.defineProperties(o, {
    'b': { get: function() { return this.a + 1; } },
    'c': { set: function(x) { this.a = x / 2; } }
});

o.c = 10; 
console.log(o.b);
``` 

## Defining Properties
- You can remove a non-inherited property by using the delete operator. The following code shows how to remove a property.
``` javascript
var myobj = new Object;
myobj.a = 5;
myobj.b = 12;

// Removes the a property, leaving myobj with only the b property.
delete myobj.a;
console.log ('a' in myobj)
```

