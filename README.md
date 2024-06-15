# JavaScript Tutorial

## let vs var vs const

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

## Objects

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

## this keyword

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

## Binding this

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

## Arrow Functions

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

## Arrow function and this

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

## Array.map

```js
const colors = ["red", "green", "blue"];
const items = colors.map((color) => `<li>${color}</li>`);
console.log(items);
```

## Object Destructuring

```js
const address = {
  street: "",
  city: "",
  country: "",
};

const { street, city, country } = address; // Accessing all object items
const { street } = address; // Accessing one object item
const { street: st } = address; // Accessing object items by assigning different name
```

## Spread Operator

On arrays

```js
const first = [1, 2, 3];
const second = [5, 6, 7];

const combined = first.concat(second); //Primitive and tiresome
const newcombined = [...first, 4, ...second, 8];

const clone = [...first];
```

On objects:

```js
const first = { name: "Amardip" };
const second = { job: "Investment Banker" };

const third = { ...first, ...second }; // Combining

first = { ...first, name: "Amardip Banerjee" }; // Modifying values
```

## Classes

Class defienes the blueprint of an object.

```js
class Person {
  constructor(name) {
    this.name = name;
  }
  walk() {
    console.log(`${this.name} is walking now!`);
  }
}

const person = new Person("Amardip");
```

## Inheritance

```js
class Person {
  constructor(name) {
    this.name = name;
  }
  walk() {
    console.log(`${this.name} is walking now!`);
  }
}

const Investmentbanker extends Person{
    constructor(name, deal){
        super(name);
        this.deal = deal;
    }
    deal() {
        console.log(`${this.name} is dealing with ${this.deal}!`);
    }
}

const ib = new Investmentbanker("Amardip", "ONGC");
```

## Modules

person.js

```js
export class Person {
  constructor(name) {
    this.name = name;
  }
  walk() {
    console.log(`${this.name} is walking now!`);
  }
}
```

ibs.js

```js
import {Person} from './person'

export const Investmentbanker extends Person{
    constructor(name, deal){
        super(name);
        this.deal = deal;
    }
    deal() {
        console.log(`${this.name} is dealing with ${this.deal}!`);
    }
}
```

index.js

```js
import { Investmentbanker } from "./ibs";

const ib = new Investmentbanker("Amardip", "ONGC");
```

Please note that these are named exports.

## Default Exports

person.js

```js
export default class Person {
  constructor(name) {
    this.name = name;
  }
  walk() {
    console.log(`${this.name} is walking now!`);
  }
}
```

ibs.js

```js
import Person from './person'

export default const Investmentbanker extends Person{
    constructor(name, deal){
        super(name);
        this.deal = deal;
    }
    deal() {
        console.log(`${this.name} is dealing with ${this.deal}!`);
    }
}
```

index.js

```js
import Investmentbanker from "./ibs";

const ib = new Investmentbanker("Amardip", "ONGC");
```

In case of default exports we may use different names. For example we may use 'Human' instead of 'Person' in ibs.js file.
