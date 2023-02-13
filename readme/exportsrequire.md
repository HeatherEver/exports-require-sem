start with learning objectives!

- understand that in NodeJS, each file is treated as a separate "module"
- know that module is an object that represents the current module
- know how require is a function used to include modules from other files within the current file
- know that module.exports is the value returned when the module is required elsewhere

---

---

---

_create 2 files_

I might want access to something i have in file1 in file2! Let's have a look how i could do that...

in _file1_ create:

```javascript
const name = "Heather";

module.exports = name;
```

in _file2_ create:

```javascript
const name = require("./file1.js");

console.log(name);
```

---

---

---

---

While things are simple show that we can change the name of the variable in _file2_

**make the students guess what will happen if we change the variable name**

It does _not_ need to match the variable name in the exporting file.

```javascript
const mystery = require("./file1.js");

console.log(mystery);
```

---

---

---

---

_let's go through what's happening under the hood_

Just like `console` is an object that is made available to us to use. _`module`_ is also an object we can _refer to in our files we run code with_

in _file1_

```javascript
console.log(module);
```

Show that it has an _`exports`_ property that we can use.

So if we remove our _`export` statement_ from _file1_ and run _file2_ we will see an empty object

---

---

---

---

What if we have _multiple_ things we want to export?

_file1_

```javascript
const name1 = "heather";
const name2 = "eli";

module.exports = name1;
module.exports = name2;
```

_file2_

```javascript
const mystery = require("./file1.js");

console.log(mystery); // logs 'eli'
```

**WHY is it eli?!...**

**HOW** can we export more than one thing?

in an object!!!

---

---

---

---

_// file1.js_

```javascript
const name1 = "heather";
const name2 = "eli";
const multipleNames = { name1: name1, name2: name2 }; // use long-hand syntax for clarity here

module.exports = multipleNames;
```

_file2_

```javascript
const mystery = require("./file1.js");
console.log(mystery); // logs {name1: 'heather', name2: 'eli'}

console.log(mystery.name1); // heather
console.log(mystery.name2); // eli
```

---

---

---

---

_FUNCTIONS_

_file1_

```javascript
const sayHello = function () {
  console.log("hello");
};

module.exports = sayHello;
```

_file2_

```javascript
const mystery = require("./file1.js");
console.log(mystery); // logs [Function sayHello]
```

---

_ASK_ what will be logged?!?!

Show how we actually get `[Function sayHello]` because we _haven't used_ the exported function - the _uninvoked_ function is exported.

---

---

---

To get the 'hello' console.log, we have to _use_ the required in function - show this too

---

---

---

**MAKE another function goodbye**

_file1_

```javascript
const sayHello = function () {
  console.log("hello");
};

sayGoodbye = function () {
  console.log("goodbye");
};

module.exports = { sayHello: sayHello, sayGoodbye: sayGoodbye };
```

_file2_

```javascript
const mystery = require("./file1.js");
console.log(mystery); // logs {sayHello: [Function sayHello], sayGoodbye: [Function sayGoodbye] }
```

Show can you can use short-hand when declaring objects if you want the new key to be the same as the variable name. Mention that this is not unique to exporting and can be used anywhere that an object is declared. (Unless they are very strong, leave object destructuring for another day)

**file1.js**

```javascript
const sayHello = function () {
  console.log("hello");
};

sayGoodbye = function () {
  console.log("goodbye");
};

module.exports = { sayHello, sayGoodbye };
```
