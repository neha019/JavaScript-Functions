# What is Observables ? 

Observables are an array which throws items/data synchronously and asynchronously. 

> ## _Observables are lazy collections of multiple values over time._ 

It is an object with three functions : 
- next() => Observables calls this function whenever a new value is appended in the cache/queue.
- error() => Observables calls this function whenever a new error is logged in the code.
- complete() => Observables calls this function when a job is completed.

Observables can have mu;tiple values over time. 