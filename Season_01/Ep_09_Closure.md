# Closures in JavaScript

Function bundled along with it's lexical scope is closure.

JavaScript has a lexcial scope environment. If a function needs to access a variable, it first goes to its local memory. When it does not find it there, it goes to the memory of its lexical parent. See Below code, Over here function y along with its lexical scope i.e. (function x) would be called a closure.
Sample code:

```js
function x() {
  var a = 7;
  function y() {
    console.log(a);
  }
  y();
}
x();
```

Sample output:

```
7
```

Dev tools snap:

![closure-dev-tools.png](../images/closure.jpg)
# Closures in JavaScript

## What is a Closure?

- A **closure** is a function **bound together** with its **lexical environment**.
- In simpler terms:
  - A closure is **a function along with its surrounding (lexical) scope**.
- This allows the function to **access variables** from its **outer (enclosing) function**, even after the outer function has finished execution.

---

## MDN Definition

> A **closure** is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment).  
> In other words, a closure gives you access to an outer function’s scope from an inner function.  
> In JavaScript, closures are created every time a function is created, at function creation time.

---

## Example Observation from Debugging

- If you pause execution (e.g., at `console.log(a);` inside a nested function), and inspect the **Scopes** in Developer Tools:
  - You will see the function forming a **closure** with its **lexical parent**.
  - For instance, if `y()` is defined inside `x()`, then `y()` has a closure with `x()`.

---

## Functions are First-Class Citizens in JavaScript

- JavaScript treats functions as **first-class objects**:
  - They can be **assigned to variables**.
  - They can be **passed as arguments** to other functions.
  - They can be **returned** from other functions.

---

## Example (Assuming `x` is already defined)

```js
function x() {
  let a = 10;
  function y() {
    console.log(a); // y() has access to x()'s variable
  }
  return y;
}

const z = x(); // x() returns y, which closes over `a`
z(); // 10 — closure allows access to a even after x() has finished


```js
x(function y() {
  console.log(a);
});
```

Moreover, we are also allowed to return a function from a function in JavaScript. This is where the concept of closures kind of complicate things.

Sample code:

```js
function x() {
  var a = 7;
  function y() {
    console.log(a);
  }
  return y;
}
var z = x();
z();
```

Sample output:

```
7
```

Now here **closure** comes into picture. When a function is returned from another function, they still maintain their lexical scope. They remember where they were actually present. Meaning, `y()` remembers where it came from. It means that when we returned `y()`, it's not just that the function code was returned, but a closure enclosed function along with its lexical scope was returned.

The following code snippet is equivalent to the last one.

```js
function x() {
  var a = 7;
  return function y() {
    console.log(a);
  };
}
var z = x();
z();
```

Whenever we return a function, the references to the data members as part of the closure are retained instead of being garbage collected.
- A closure is a function that has access to its outer function scope even after the function has returned. Meaning, A closure can remember and access variables and arguments reference of its outer function even after the function has returned.
_Uses of **Closures**:_

- Module Design Pattern
- Currying
- Functions like once
- Memoize
- Maintaining state in async world
- setTimeouts
- Iterators
- and many more...

# Advantages of Closure:

Certainly! Let's explore examples for each of the advantages you've mentioned:

## Module Design Pattern:

- The module design pattern allows us to encapsulate related functionality into a single module or file. It helps organize code, prevent global namespace pollution, and promotes reusability.

Example: Suppose we're building a web application, and we want to create a module for handling user authentication. We can create a auth.js module that exports functions like login, logout, and getUserInfo.
```
// auth.js
const authModule = (function () {
  let loggedInUser = null;

  function login(username, password) {
    // Authenticate user logic...
    loggedInUser = username;
  }

  function logout() {
    loggedInUser = null;
  }

  function getUserInfo() {
    return loggedInUser;
  }

  return {
    login,
    logout,
    getUserInfo,
  };
})();

// Usage
authModule.login('john_doe', 'secret');
console.log(authModule.getUserInfo()); // 'john_doe'
```
## Currying:

- Currying is a technique where a function that takes multiple arguments is transformed into a series of functions that take one argument each. It enables partial function application and enhances code flexibility.

Example: Let's create a curried function to calculate the total price of items with tax.
```
const calculateTotalPrice = (taxRate) => (price) => price + price * (taxRate / 100);

const calculateSalesTax = calculateTotalPrice(8); // 8% sales tax
const totalPrice = calculateSalesTax(100); // Price with tax
console.log(totalPrice); // 108
```
## Memoization:

- Memoization optimizes expensive function calls by caching their results. It's useful for recursive or repetitive computations.

Example: Implement a memoized Fibonacci function.
```
function fibonacci(n, memo = {}) {
  if (n in memo) return memo[n];
  if (n <= 1) return n;

  memo[n] = fibonacci(n - 1, memo) + fibonacci(n - 2, memo);
  return memo[n];
}

console.log(fibonacci(10)); // 55
```
## Data Hiding and Encapsulation:

- Encapsulation hides the internal details of an object and exposes only necessary methods and properties. It improves code maintainability and security.

Example: Create a Person class with private properties.
```
class Person {
  #name; // Private field

  constructor(name) {
    this.#name = name;
  }

  getName() {
    return this.#name;
  }
}

const person = new Person('Alice');
console.log(person.getName()); // 'Alice'
// console.log(person.#name); // Error: Private field '#name' must be declared in an enclosing class
```
## setTimeouts:

setTimeout allows scheduling a function to run after a specified delay. It's commonly used for asynchronous tasks, animations, and event handling.

Example: Delayed message display.
```
function showMessage(message, delay) {
  setTimeout(() => {
    console.log(message);
  }, delay);
}

showMessage('Hello, world!', 2000); // Display after 2 seconds
```
These examples demonstrate the power and versatility of closures in JavaScript! 🚀

## Disadvantages of Closure:

- Over consumption of memory
- Memory Leak
- Freeze browser
