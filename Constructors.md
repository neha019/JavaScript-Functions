# Constructor 

Constructor method is used for creating and initializing an object created within a class.

## Syntax 
> constructor([arguments]) {
    ....
} 

Example : 
```javascript 
class Circle extends Polygon {
    constructor(length) {
        super(length, length);
        this.name='Circle';
    }

    get area() {
        return this.height*this.width;
    } 

    set area(value) {
        this.area=value;
    }
} 
``` 

```javascript 
function Identity(name, surname) {
    this.name=name;
    this.surname=surname;
}

var credentials=new Identity("neha", "verma");
console.log('Name is : ',credentials.name);
console.log('Surname is : ',credentials.surname); 
``` 
