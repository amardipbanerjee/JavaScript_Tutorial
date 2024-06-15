# JavaScript Tutorial

### let vs var vs const

'var' has a global scope but is limited to the function inside which it is defined.
'let' and 'const' both have a block level scope.
'const' defines a constant in JavaScript.

```js
function sayHello() {
  for (let i = 0; i < 5; i++) {
    console.log(i);
  }
  console.log(i); // Error i is not deifned
  for (var j = 0; j < 5; j++) {
    console.log(j);
  }
  console.log(j); // No Error
  const k = 1;
}

console.log(k); // Error k is not deifned
```
