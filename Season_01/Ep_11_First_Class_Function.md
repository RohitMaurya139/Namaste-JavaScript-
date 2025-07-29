# First Class Functions

- What is an Anonymous function?
- What is a First Class Function?
- Function Statement vs. Function Expression vs. Function Declaration

## JavaScript Function Concepts

---

## 1. What is an Anonymous Function?

- An **Anonymous Function** is a function **without a name**.
- It is often used in places where functions are used **as values**, like:
  - Passing as arguments
  - Assigning to variables
  - In IIFE (Immediately Invoked Function Expressions)

### Example:

```js
const greet = function() {
  console.log("Hello");
};
greet(); // Output: Hello
```
- Anonymous functions cannot be called by name, because they don't have one.

- Common in callbacks and functional programming.

## 2. What is a First-Class Function?
**First Class Functions**
- The ability to use functions as values is known as First Class Functions. 
- In JavaScript, functions are first-class citizens (aka first-class objects).
-  The concept of First Class Functions and First Class Citizens is the same.

    - This means functions can be:

        - Assigned to variables

        - Passed as arguments

        - Returned from other functions

        - Stored in data structures

Example:
```
function greet() {
  return "Hello";
}


function callFunc(fn) {
  console.log(fn()); // Calls the function passed as argument
}


callFunc(greet); // Output: Hello
```
Because of this flexibility, JavaScript supports higher-order functions (functions that operate on other functions).

## 3. Function Statement vs. Function Expression vs. Function Declaration
### ✅ Function Statement (a.k.a. Function Declaration)
- A standard way of defining a named function using the function keyword.

- Hoisted completely (both function name and definition).

```
function sayHello() {
  console.log("Hello");
}
```
Can be invoked before its declaration due to hoisting.

## ✅ Function Expression
- A function defined by assigning it to a variable.

- Can be named or anonymous.

- Only the variable name is hoisted (not the function definition).

```
const sayHi = function() {
  console.log("Hi");
};
```
- Cannot be called before the definition (throws TypeError).

| Feature                | Function Declaration | Function Expression          |
| ---------------------- | -------------------- | ---------------------------- |
| Hoisting               | Fully hoisted        | Only variable is hoisted     |
| Can call before define | Yes                  | No                           |
| Syntax                 | `function func() {}` | `const func = function() {}` |
| Named function         | Required             | Can be anonymous or named    |

# Summary
- Anonymous Function: Function with no name.

- First-Class Function: Functions treated like any other value.

- Function Declaration: Fully hoisted and can be called early.

- Function Expression: Not hoisted with definition; more flexible.