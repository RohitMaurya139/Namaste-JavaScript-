
### The Scope Chain - Scope & Lexical Environment

Scope in JavaScript is directly related to Lexical Environment. The Lexical Environment is a very classic concept in JavaScript.

Sample code:

```js
// CASE 1
function a() {
  console.log(b); // 10
  // Instead of printing undefined it prints 10, So somehow this a function could access the variable b outside the function scope.
}
var b = 10;
a();
```

Sample output:

```
10
```

## Justification:

- When the function is invoked as `a();`, the JavaScript engine performs a variable lookup for `b`.
- It first looks for `b` in the **local memory space** of the function `a()`.
- If `b` is not found locally, the engine moves **one level up**, which is the **outer lexical environment**.
- In this case, the outer level is the **global memory space**, where it finds `b = 10`.
- If `b` were **not available** in the global scope either, the engine would:
  - Continue searching **up the scope chain** (one level at a time).
  - Repeat this process until it:
    - **Finds the variable**, or
    - **Reaches the global scope** and still doesn’t find it.
- If the variable is not found anywhere in the chain, JavaScript throws a **ReferenceError**.

> This entire mechanism is called **Lexical Scoping** or **Scope Chain Resolution**.


Sample code:

```js
function a() {
  c();
  function c() {
    console.log(b); // 10
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
// CASE 3
function a() {
  c();
  function c() {
    var b = 100;
    console.log(b); // 100
  }
}
var b = 10;
a();
```
```
// CASE 4
function a() {
  var b = 10;
  c();
  function c() {
    console.log(b); // 10
  }
}
a();
console.log(b); // Error, Not Defined
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

## Lexical Environment in JavaScript

- **Lexical Environment** = Local Memory + Reference to the Lexical Environment of its parent.
- The term **"Lexical"** refers to a structure that is **hierarchical** or **sequential** in nature.

---

## Code-Level Understanding

- In the context of the code:
  - `c()` is **lexically** inside `a()`.
  - `a()` is **lexically** inside the **global scope**.
- This means that the **location of a function or variable** in the source code determines its **lexical environment**.

---

## Execution Context Relationship

- Every time a new **Execution Context** is created:
  - Its **memory component** includes a **reference to the parent Lexical Environment**.
- For the **Global Execution Context**, this reference is **null** because it has no parent.

---

## Visualization

- This relationship can be **visualized** like a **chain of environments**, from inner to outer:


![lexical-env-visualization-js.png](../images/lexical.jpg)


- When a variable is **not found** in the current **local memory**, the JavaScript engine:
  - Searches for it in the **lexical parent environment**.
  - Continues this process **up the chain** until:
    - The variable is found, or
    - The reference reaches `null` (i.e., **global scope is exhausted**).

---

## Scope Chain

- The **Scope Chain** is the **chain of all Lexical Environments** linked through their parent references.
- This mechanism is what powers **variable lookup** in JavaScript.

---

## Execution Context and Lexical Environment

- Whenever an **Execution Context** is created:
  - A **Lexical Environment** is also created.
  - This is part of the **memory component** of the Execution Context.
- The Lexical Environment includes:
  - Local variables/functions.
  - A **reference to the Lexical Environment of the parent context**.
- In the case of the **Global Execution Context (GEC)**:
  - The parent reference points to `null`.

---

## Variable Not Defined

> A variable is considered **"not defined"** when the Scope Chain is **fully traversed** and the variable is still **not found**.

---

## Developer Tools

- The **Scope Chain** can be **visualized** using the **developer tools** of any modern browser.
  - Go to **Sources tab** > open the file > add a breakpoint > inspect **Scopes**.



![scope-chain-dev-tools.png](../images/lexical2.jpg)

---
```
function a() {
  function c() {
    // logic here
  }
  c(); // c is lexically inside a
} // a is lexically inside global execution
```
> - Lexical or Static scope refers to the accessibility of variables, functions and object based on physical location in source code.
```
Global {
    Outer {
        Inner
    }
}
// Inner is surrounded by lexical scope of Outer
```
> - TLDR; An inner function can access variables which are in outer functions even if inner function is nested deep. In any other case, a function can't access variables not in its scope.

