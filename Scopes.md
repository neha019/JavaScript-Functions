# JavaScript Scopes

> ##  What is Scope ?
Scope is the accessibility of variables, functions, and objects in some particular part of your code during runtime. In other words, scope determines the visibility of variables and other resources in areas of your code.  

JavaScript has two scopes :
- _Global Scope_ :
Any Variable declared outside of a function is accessible anywhere in th code.

- _Local Scope_ :
Any varaiable declared within a function is only accessible from that function and any nested functions.

Note : Local Scope is created by functions in JavaScript. It is also called as **_function scope_**.

**Example of Global Scope :**
```JavaScript
    var name = 'Hammad';

    console.log(name); 

    function logName() {
        console.log(name);
    }

    logName(); 
```
**Output :**  
> - **console.log(name)** in the global scope will print _Hammad_ in console  
> - **console.log(name)** within a function will also print _Hammad_ in console   

>Because function **_logName_** will log for name variable within its _local scope_, if not found it will look in _global scope_. 

**Example of Local Scope :**
```JavaScript
function someFunction() {
    var x="test";
    function someOtherFunction() {
        var x="test1";
        console.log(x);
    }
    console.log(x);
}


function anotherFunction() {
    return "I am in global scope";
}
someFunction();
anotherFunction();
```
**Output :**  
>someFunction() ---  _test1_ and _test_  
anotherFunction() --- I am in global scope  

**Points To Remember :**
- The JavaScript interpreter works from the currently executing scope and works it way out until it finds the variable in question. If the variable is not found in any scope, then an exception is thrown.

- This type of lookup is called **_lexical(static) scope_**. The scope of a variable is defined by its location within the source code, and nested functions have access to variables declared in their outer scope. 

> In JavaScript, variables with same name can be defined at multi layers of nested scope. This  type of  behaviour is called **_Shadowing_**, the inner variable shadows the outer.

**Example of Shadowing :**
```JavaScript
var test = "I'm global";

function testScope() {
  var test = "I'm local";

  console.log (test);     
}

testScope();
console.log(test);
```
**Output :**  
>testScope() --- I'm local  
console.log(test) --- I'm global  



