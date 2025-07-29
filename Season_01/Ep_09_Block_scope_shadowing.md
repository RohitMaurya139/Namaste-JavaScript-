### Block Scope & Shadowing in JS

`let` and `const` are **Block Scoped**.
- Block aka compound statement is used to group JS statements together into 1 group. We group them within {...}
The following is a perfectly valid JS code.

```js
{
}
```

## What is a Block?

- Anything enclosed between `{` and `}` is called a **block**.
- Even if it contains **no code**, it is still considered a block.
- Blocks are also known as **Compound Statements**.

---

## Why Use a Block / Compound Statement?

- JavaScript often expects **a single statement** in certain places (e.g., after an `if` condition).
- A **Compound Statement** (block) allows us to **group multiple statements** and treat them as **one**.
- This is helpful in control flow constructs like `if`, `for`, `while`, etc.

### Example:

```js
if (true)
  console.log("One line only"); // ✅ Works

if (true) {
  // ✅ Block allows multiple statements
  console.log("First line");
  console.log("Second line");
}


```js
{
  var a = 10;
  let b = 20;
  const c = 30;
}
```

![let-const-block-scoped-dev-tools.png](../images/scope.jpg)

As shown in the image above, we've got `b` and `c` inside the `Block` scope. They are hoisted and assigned `undefined`. They are hoisted in a separate memory space which is reserved for their block. But, we see that `a` is hoisted inside the `Global` scope.

_`let` and `const` are block scoped_, which means that a separate memory space is reserved for the block of which the `let` and `const` declarations are a part of.

We would be able to access `a` outside the block, since it's hoisted as part of the `Global` scope. That's not the case for the `let` and `const` declarations.

**Shadowing**

Sample code:

```js
var a = 100;
{
  var a = 10;
  console.log(a);
}
console.log(a);
```

Sample output:

```
10
10
```

The inner `a` shadowed the outer `a` and the value was also overridden, reason for which we got the above output. This happened since both of them were pointing to the same memory location, the global memory space in this case.

Shadowing works differently in case of `let` and `const`.

Sample code:

```js
let b = 100;
{
  var b = 20;
  console.log(b);
}
console.log(b);
```

Sample output:

```
20
100
```

So, we see that the inner `b` shadowed the outer `b`, but since both of these are referring to different memory spaces, the inner `b` didn't override the outer `b`. If we analyze the code using developer tools, we see that the inner `b` is part of the `Block` scope, while the outer `b` is part of the `Script` scope. According to the dev tools, we see that there are 3 memory spaces or scopes, namely `Block`, `Script` and `Global`.

**Illegal Shadowing**

Sample code:

```js
let a = 20;
{
  var a = 200;
}
```

We'll face the following error in the above code.

```
Uncaught SyntaxError: Identifier 'a' has already been declared
```

This is an example of **Illegal Shadowing**.

But, if we tried the same thing with both the declarations being of either `let` or `const`, then legal shadowing could have occurred.

But the following is also a case of legal shadowing.

```js
var a = 200;
{
  let a = 20;
}
```

Let's dig deep with the earlier code.

```js
let a = 20;
{
  var a = 200;
}
```

If a data member is attempting to shadow another data member, it shouldn't cross the boundary of its scope. In a particular scope, `let` cannot be re-declared.

Now, `var` is **function scoped**. This means that the following piece of code is totally valid.

```js
let a = 20;
function x() {
  var a = 200;
}
```

**Block Scope** follows **Lexical Scope**.

Also, the concept of scope in case of arrow functions is exactly the same as what we encounter in case of normal functions in JavaScript.

---