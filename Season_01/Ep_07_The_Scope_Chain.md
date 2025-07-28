
### The Scope Chain - Scope & Lexical Environment

Scope in JavaScript is directly related to Lexical Environment. The Lexical Environment is a very classic concept in JavaScript.

Sample code:

```js
function a() {
  console.log(b);
}
var b = 10;
a();
```

Sample output:

```
10
```

Justification:

When the function is invoked as `a();`, the JavaScript engine looks for `b` in the local memory space of `a()`. Failing to find it, it then searches for the same a level up, the global memory space in this case, and finds the value `10` assigned to `b`.

If, suppose, `b` weren't available in the upper level, and there were more levels preceding the current level, it'll search for `b` in the upper levels, till either it finds it or we run out of levels, which happens when one reaches the global memory space.

Sample code:

```js
function a() {
  c();
  function c() {
    console.log(b);
  }
}
var b = 10;
a();
```

Sample output:

```
10
```

Let's take another example.

Sample code:

```js
function a() {
  var b = 10;
  c();
  function c() {}
}
a();
console.log(b);
```

The above code will face the following error:

```
Uncaught ReferenceError: b is not defined at ...
```

Here's where scope comes into picture.

> Scope is basically where you can access a particular data member.

There are 2 aspects to Scope:

- What is the scope of this (referring to the current) variable? Meaning, where can I access this variable?
- Is this variable inside the local (referring to the Local Execution Context) scope?

The Scope is directly dependent on the Lexical Environment.

> _Whenever an **Execution Context** is created, a **Lexical Environment** is also created._

Lexical Environment is the local memory along with the Lexical Environment of its parent. Lexical, as a term, means in hierarchy, or in a sequence.

Corresponding to the above code block, we can say that the `c()` is lexically sitting inside `a()`. In terms of code, it's basically where a particular data member is located. Corresponding to that, we can say that `a()` is lexically inside the global scope.

Whenever a new Execution Context is created, in the memory component of this Execution Context, we also get a reference to the Lexical Environment to its parent. In case of the Global Execution Context, this reference points to `null`.

It can be visualized by the diagram below, in correspondence to the above code.

![lexical-env-visualization-js.png](https://i.ibb.co/Tm4WsH9/lexical-env-visualization-js.png)

So, technically when a variable is not found in the current local memory, the engine searches for that variable in the reference which points to the lexical parent and continues this process until the variable is found or we hit `null`. This search mechanism works on the basis of the **Scope Chain**. So, _the **Scope Chain** is the chain of all these lexical environments and their parent references._

So, whenever an Execution Context is created, a Lexical Environment is also created, which is a part of the memory component of this Execution Context. This Lexical Environment is actually a reference to the memory component of the lexical parent of the current Execution Context and in case of the **GEC** (Global Execution Context), this reference points to `null`.

> So, a variable is `not defined` when this **Scope Chain** is exhausted and the variable is not found.

The **Scope Chain** can be visualized by using the developer tools of any modern browser.

![scope-chain-dev-tools.png](https://i.ibb.co/pwKFHZK/scope-chain-dev-pngtools.)

---