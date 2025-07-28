### Hoisting in JavaScript

Let's take 2 code blocks for example.

First block:

```js
getName(); // Namaste Javascript
console.log(x); // undefined
var x = 7;
function getName() {
  console.log("Namaste Javascript");
}
```

Output:

```
Namaste JavaScript
undefined
```

Second block:

```js
getName(); // Namaste JavaScript
console.log(x); // Uncaught Reference: x is not defined.
console.log(getName); // f getName(){ console.log("Namaste JavaScript); }
function getName() {
  console.log("Namaste JavaScript");
}
}
```

Output:

```
Namaste JavaScript
Uncaught Reference: x is not defined.
 f getName(){ console.log("Namaste JavaScript); }
```

In most programming languages, code similar to the second block will throw errors, but that's not the case in JavaScript.

If we remove the statement `var x = 7;` from the second code block, which becomes like this:

```js
getName(); // Uncaught TypeError: getName is not a function
console.log(getName);
var getName = function () {
  console.log("Namaste JavaScript");
};
// The code won't execute as the first line itself throws an TypeError.
```

It will now throw the following error:

```
Uncaught TypeError: getName is not a function because getName is variable not function
```

Now, **not defined** and **undefined** are 2 different things.

All these scenarios are due to something called **Hoisting** in JavaScript.

**Hoisting**

- **Hoisting** is a phenomena in JavaScript by which we can access variables and functions even before initializing them.
- **Hoisting** is a concept which enables us to extract values of variables and functions even before initialising/assigning value without getting error and this is happening due to the 1st phase (memory creation phase) of the Execution Context.

- The result of **Hoisting**, i.e., the memory allocation that happens due to which we are able to access variables and functions even before initializing them, can be viewed in the developer tools. Also, we have a debugger in the developer tools by which we can stop execution of our code and check for ourselves the value that is stored against the variables and functions even before start of the execution.