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

### Objects

Functions inside objects in OOPs are called methods.

```js
const person = {
  name: "Mosh",
  walk: function () {},
  talk() {}, // ES6 way of deifining function inside object
};

// Dot notation of accessing
person.talk();
person.name = "";

// Bracket notation of accessing
const targetMember = "name";
person["name"] = "John";
person[targetMember.value] = "John";
```

Please note that we use the bracket notation when we do not previously know what member of value we are going to access. For example if the member to be changed is being input by an user in a form.

### this keyword

Here 'this' will return a reference to the person object.

```js
const person = {
  name: "Mosh",
  walk() {
    console.log(this);
  },
};

person.walk();
```

However 'this' keyword in JavaScript behaves differently than other programming languages.

```js
const person = {
  name: "Mosh",
  walk() {
    console.log(this);
  },
};

person.walk();

const walk = person.walk; // Storing reference to the function not the object
walk(); // Returns undeifned
```

The value of 'this' keyword is determined by how a function is called. If we call a functionas a method in an object, it returns a reference to the object. <br/> However if we call a function as a standalone object or outside of an object, 'this' will return the global obect that is the window object in browsers. But in this case we get 'undefined' because the code is executed in JavaScript strict mode which is to execute a code in a more protective way to prevent potential problems.
