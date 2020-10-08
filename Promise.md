# Promise

## What is Promise ?
The Promise object represents the eventual completion (or failure) of an asynchronous operation, and its resulting value.

A Promise is a returned object to which we attach callbacks , instead of passing callbacks into a function.

> A _Promise_ is one of these states :
> - _pending_ : initial state , neither fulfilled nor rejected.
> - _fulfilled_ : meaning that the operation commpleted successfully.
> - _rejected_ : meaning that the operation failed.

As the Promise.prototype.then() and Promise.prototype.catch() methods return promises , they can be chained .

![](promises.png?raw=true)


**Old Style of passing callbacks in function :**

```javascript
function doSomethingOldStyle(successCallback, failureCallback) {
  console.log("It is done.");
  // Succeed half of the time.
  if (Math.random() > .5) {
    successCallback("SUCCESS")
  } else {
    failureCallback("FAILURE")
  }
}

function successCallback(result) {
  console.log("It succeeded with " + result);
}

function failureCallback(error) {
  console.log("It failed with " + error);
}

doSomethingOldStyle(successCallback, failureCallback);
``` 

**The constructor syntax for a promise object is :** 

```JavaScript
let promise = new Promise(function(resolve, reject) {
  // executor (the producing code, "singer")
});
``` 
_promise_ object has internal properties :

- state - initially is "_pending_" , then changes to "_fulfilled_" or "_rejected_".
- result - an arbitrary value initially "_undefined_".

When the executor finishes the job , it should call one of :
- resolve(value) - to indicate the job is finished successfully :
    - sets state to "_fulfilled_".
    - sets result to value.
- reject(error) - to indicate that an error occured :
    - sets state to "_rejected_".
    - sets result to error.

**An example where executor rejects promise with an error :**

```javascript
let promise = new Promise(function(resolve, reject) {
  // after 1 second signal that the job is finished with an error
  setTimeout(() => reject(new Error("Whoops!")), 1000);
});
```

**Promise.all()** 

Promise.all(iterable) method returns a single _Promise_ that resolves when all of Promises in the iterable argument have resolved or when the iterable argument contains no promises. It rejects with the reason of the first promise that rejects.

**Syntax :** 
  >Promise.all(iterable); 

**Return Value :** 
- An already resolved Promise if the iterable passed is empty.
- An asynchronously resolved Promise if the iterable passed contains no promises. Note, Google Chrome 58 returns an already resolved promise in this case.
- A pending Promise in all other cases. 


**Example of Promise.all() :** 
```javascript 
var promise1 = Promise.resolve(3);
var promise2 = 42;
var promise3 = new Promise(function(resolve, reject) {
  setTimeout(resolve, 100, 'foo');
});

Promise.all([promise1, promise2, promise3]).then(function(values) {
  console.log(values);
});
// expected output: Array [3, 42, "foo"] 
``` 

> **Promise.prototype.catch()** 

The _catch()_ returns a promise which deals with rejected values only. It behaves same as calling _.then()_.

Calling _object.catch()_ internally calls _object.then()_.

> **Syntax :**  
``` 
p.catch(onRejected);

p.catch(function(reason) {
   // rejection
}); 
``` 

**Example of Promise.prototype.catch() :**

```javascript 
var promise1 = new Promise(function(resolve, reject) {
  throw 'Uh-oh!';
});

promise1.catch(function(error) {
  console.log(error);
});
// expected output: Uh-oh! 
``` 

**Promise.prototype.finally() :** 

The _finally()_ method returns a Promise, whether the promise is settled, fulfilled or rejected. This lets you avoid duplicating code in both the promise's _then()_ and _catch()_ handlers.

**Syntax :**

``` 
p.finally(onFinally);

p.finally(function() {
   // settled (fulfilled or rejected)
}); 
``` 

**Example of Promise.prototype.finally() :** 

```javascript 
function getData() {
  var promise=new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('success');
    }, 2000);
  });
}

var x=getData();

x.then(() => {
  console.log('success');
})
.catch(() => {
  console.log('error');
})
.finally(() => {
  console.log('finally function block executed somehow');
}) 
``` 

