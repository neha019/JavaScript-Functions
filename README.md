# JavaScript-Functions

## Function Scope

Functions defined in global scope can access all variables at global scope level. 
Functions defined inside another function have access to all the variables of its parent function.

_Example Given_:
`
var name = 'Neha';
    surname: 'Verma';

// This function is defined in the global scope
function getName() {
  return name + surname;
}

getName(); // Returns Neha Verma

// A nested function example
function getScore() {
  var num1 = 2,
      num2 = 3;
  
  function add() {
    return name + ' scored ' + (num1 + num2);
  }
  
  return add();
}

getScore(); // Returns "Neha scored 5"
`

