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
walk(); // Returns undeifned or window object
```

The value of 'this' keyword is determined by how a function is called. If we call a functionas a method in an object, it returns a reference to the object. <br/><br/> However if we call a function as a standalone object or outside of an object, 'this' will return the global obect that is the window object in browsers. But in this case we get 'undefined' because the code is executed in JavaScript strict mode which is to execute a code in a more protective way to prevent potential problems.

### Binding this

Every method or function in JavScript is also an object. They have properties and methods. So we can use the '.bind' propety to bind a function to an object, which, in this case is the 'person' object.

```js
const person = {
  name: "Mosh",
  walk() {
    console.log(this);
  },
};

person.walk();

const walk = person.walk.bind(person);
walk();
```

With the bind methos we set the value of 'this' parmanently. It does depend on the argument we pass (in this case, the 'person' object).

### Arrow Functions

Arrow functions are in ES6 module which helps to create a clean code specially in filter and map methods.
<br/>
<br/>
Arrow function without any parameter:

```js
const testfunc = () => {
  console.log("hi");
  return 5;
};
```

Arrow function without 1 parameter and single line:

```js
const testfunc = value => return value * value;
```

### Arrow function and this

When we define a callback function inside a method in an object, the callback function is treated as a standalone function.

```js
const person = {
  talk() {
    setTimeout(function () {
      console.log("this", this); // gives the window object
    }, 1000);
  },
};

person.talk();
```

Contemporary solution:

```js
const person = {
    var self = this;
  talk() {
    setTimeout(function () {
      console.log("self", self); // gives reference to window object
    }, 1000);
  },
};

person.talk();
```

Arrow function inherit the this keyword by default:

```js
const person = {
  talk() {
    setTimeout(() => {
      console.log("this", this); // gives reference to window object
    }, 1000);
  },
};

person.talk();
```

### Array.map

```js
const colors = ["red", "green", "blue"];
const items = colors.map((color) => `<li>${color}</li>`);
console.log(items);
```

### Object Destructuring
