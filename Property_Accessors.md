# Property Accessors

> ## what is property accessor ?

Property Accessors provide access to an object's properties by using dot notation or bracket notation.

```javascript
var obj={};
obj['firstname']='neha';
obj['lastname']='verma'
console.log(obj.lastname); // verma

obj={ 'firstname': 'neha', 'lastname': 'verma'};
console.log(obj['firstname']); //neha
``` 

> ## Dot Notation 

```
get=object.property;
object.property=set;
``` 
_property_ must be a valid identifier including underscore(_) and dollar($) sign that cannot start with a number. For example : obj.$property name is valid whereas obj.1property name is invalid.

> ## Bracket Notation 

```
get = object[property_name];
object[property_name] = set;
``` 
_property_name_ is a string. Id doesnt have to be a valid identifier. It can have any value, for example : "!foo", "1bar".

