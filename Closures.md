# CLOSURE 

> ## What is Closure ?

A Closure is a combination of functions bundled together with reference to its surrounding state (lexical environment). Closure gives access to outer functions variables from inner functions. In JavaScript, Closures are created everytime a function is created, at function creation time. The inner functions have access to variables in the outer function scope, even after the outer function has returned. Closures are asynchronous in nature.

> ### Example 
``` javascript
function showName(first, last) {
    var intro = 'My Name is ';
    function fullName() {
        return intro + first + " " + last;
    }
    return fullName()
}

var getName = showName('Neha', 'Verma');
console.log(getName);
``` 

> ## Closure's Rules and Side Effects :
1. Closures have access to the outer function’s variable even after the outer function returns: 
``` javascript
function getName(first) {
    var intro = 'full name is ';
    function lastName(last) {
        return intro + first + " " + last;
    }
    return lastName;
}

var name = getName('Neha');
name('Verma');
``` 

2. Closures store references to the outer function’s variables : 
``` javascript
function celebId() {
    var celeb = 999;
    return {
        getId = function() {
        return celeb;
        },
        setId = function(newId) {
            celeb = newId;
        }
    };
}

var id = celebId();
celebId.getId(); // 999
celebId.setId(555); // changes outer function's variable
celebId.getId(); // 555
``` 

> ### Note :
- new function lexical environment is created each time a function runs.
- lexical environment is a specification object. We can't get this object inour code and manipulate it directly. JS engine may optimize it, discard variables that are unused to save memory and perform other internal tricks.

