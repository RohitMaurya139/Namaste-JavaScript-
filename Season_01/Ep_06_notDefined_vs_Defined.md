

#  **Undefined** VS **Not Defined** in JavaScript

`undefined` is a very special keyword in JavaScript, which is not there in other languages. This keyword has a lot to do with how JavaScript code is executed.

As discussed earlier, JavaScript code is executed in a different way. It creates a **GEC** (Global Execution Context) and allocates memory to all the variables and functions (which are present at the global scope) even before a single line of code is executed. Here is where `undefined` comes into picture.

When JavaScript allocates memory to all the variables and functions, to the variables it tries to put a placeholder. `undefined` is treated like a placeholder which is placed in the memory. So, technically, `undefined` takes up some memory space. It's totally different than `not defined`.

So, while creating the memory component, the JavaScript engine allocates `undefined` to all the variables before execution begins.

Sample code:

```js
console.log(a);
var a = 7;
console.log(a);
```

Sample output:

```
undefined
7
```

So, coming to `not defined`, `not defined` refers to something which has not been allocated memory.

`undefined` can be taken as a placeholder for the time being until a value is assigned replacing this placeholder.

Sample code:

```js
var a;

if (a === undefined) {
  console.log("a is undefined");
} else {
  console.log("a is not undefined");
}
```

Sample output:

```
a is undefined
```

**_JavaScript is a loosely typed language_**. Loosely typed means that it does not attach it's variables to any specific data type. That means that the data type of the data being stored in a variable can change from time to time. In this case, JavaScript is very flexible. In strict type languages like C, C++, Java, etc., every variable is associated with a data type, that means that a variable of type `String` in Java will only be able to store data of type `String`, so on and so forth.

Sample code:

```js
var a;
console.log(a);
a = 10;
console.log(a);
a = "hello world";
console.log(a);
```

Sample output:

```
undefined
10
hello world
```

Hence, JavaScript is a loosely typed language. Loosely typed language is also termed as weakly typed language. That does not mean that JavaScript is weak in any sense though.

Also, even though `undefined` is a placeholder in JavaScript, it really is a bad practice to use it in assignments. The reason being that this could lead to a lot of inconsistencies.

```js
// bad practice
a = undefined;
```

---