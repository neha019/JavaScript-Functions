# JAVASCRIPT EVENT LOOP 

JavaScript is capable of Asynchronous operations through the single thread of execution. 

The event loop is the process of waiting in the queue to receive a message synchronously. Every time it increments the loop, it checks if the call stack is empty and then executes it.

![](callstack.png?raw=true) 

> ## Overview of major components in a browser 

![](basicarchitecture.png?raw=true) 

* **Heap** :- Objects are allocated in a heap which is just a name to denote a large mostly unstructured region of memory.

* **Stack** :- This represents the single thread provided for JavaScript code execution. Function calls form a stack of frames.

* **Web API's** :- are built on your web browser, and are able to expose data from the browser and surrounding computer environment and do useful complex things in it. They are not part of the javascript language itself, rather they are built on top of the core javascript code.  


> ## What is a CallStack ?

* The CallStack contains the list of messages(method calls) that needs to be executed right now. Each of these messages are called `Stack Frames`. 

* A new frame is created every time the runtime encounters a method call or any other scripted behaviour like an event firing.  

* If the stack takes up more space than it had assigned to it, it will result in a _"stack overflow"_ error.

**Example of CallStack :** 
```javascript 
function one(a) {
    console.log('one', a);
}

function two(b) {
    console.log('two', b);
    one(b);
}

two(10); 
``` 

The code above would be executed like this :

* Ignores all the function until it reaches _two(10)_.
* Invokes _two(10)_ function.
* Adds _two()_ function in the callstack with one argument whose value is 10.
* Adds _console.log()_ in the callstack above the previous list with a message _two_ and the value of parameter.
* Adds _one()_ in the callstack with the same argument passed in _two()_ above the previous list.
* Goes to _one()_ function and prints the message within _console.log()_ along with the value of parameter.
* Once all the code within the functions are executed synchronously, each of them gets removed from the callstack one by one.  







