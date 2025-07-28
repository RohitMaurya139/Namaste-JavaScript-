### SHORTEST JS Program

**`window` and `this` keyword**

The **shortest JavaScript program** would be **_an empty script_**.

Even though there's an empty script, still JavaScript engine is doing a lot of things behind the scenes.

Even on the execution of an empty script, a **GEC** (Global Execution Context) would be created and the JavaScript engine also sets up the memory space, though there is nothing to set as per our **empty** script.

On going to the console and typing the following:

```
> window
```

We do get some output.

Technically the `window` is like a big object with a lot of key-value pairs which typically stores different objects.

Even if our script is empty, the `window` is not.

The functions and variables in the `window` object are created by the JavaScript engine. Also, these are created into the global space, meaning we can access all these variables and functions anywhere in our JS program.

Also, just like the `window` object, the JavaScript engine creates something called `this`, which can also be logged on the console, just like the `window` object.

At the global level, the `this` points to the `window` object.

But, **What is `window`?**

`window` is actually a global object which is created along with the global execution context. So, whenever any JavaScript program is run, _a **global object** is created, a **GEC** is created, and along with that execution context a **`this`** variable is created._

Every JavaScript engine is responsible to create a global object similar to `window` on execution of a script. In case of browsers, this object is known as `window`. In case of **Node**, it's something else. But, wherever we might run our JavaScript program, one thing is for certain that _this global object would be created_, even if our script be empty.

At the global level, `this === window` returns `true` (in case of browsers).

Whenever an **Execution Context** is created, a `this` is created along with it, _even for functional execution contexts_. At the global level, the `this` points to the global object, which is `window` in case of browsers.

If we have a script with some code in it, then this global object would contain all the variables and functions which are at the global scope post **Hoisting**.

Suppose we have `var a = 10;` in the global scope, then all of the following statements are equivalent:

```js
var x = 10;
console.log(x); // 10
console.log(this.x); // 10
console.log(window.x); // 10
```

So, once again, the shortest program in JavaScript is:

```js
// Empty javaScript program but window object not empty
```

---