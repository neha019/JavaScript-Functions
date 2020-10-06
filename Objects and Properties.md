# Objects and Properties

Object properties are basically the same as ordinary JavaScript variables, except for the attachment to objects. The properties of an object define the characteristics of the object. You access the properties of an object with a simple dot-notation: 
> objectName.propertyName 

We can define a property by assigning it a value. For Example : 
```javascript 
var myCar = new Object();
myCar.make = 'Ford';
myCar.model = 'Mustang';
myCar.year = 1969; 
``` 
We can access the properties of myCar object as follows : 

```javascript 
myCar['make'] = 'Ford';
myCar['model'] = 'Mustang';
myCar['year'] = 1969; 
``` 
You can also access properties by using a string value that is stored in a variable: 

```javascript 
var propertyName = 'make';
myCar[propertyName] = 'Ford';

propertyName = 'model';
myCar[propertyName] = 'Mustang'; 
``` 



