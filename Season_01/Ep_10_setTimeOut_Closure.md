### `setTimeout` & Closures

**Interview Question:** _Print 1-5 with a lapse of 1 second between each digit._

Sample code:

```js
function x() {
  var i = 1;
  setTimeout(function () {
    console.log(i);
  }, 3000);
}
x();
```

The above code prints `1` after 3 seconds.

Sample code:

```js
function x() {
  var i = 1;
  setTimeout(function () {
    console.log(i);
  }, 3000);
  console.log("Namaste JavaScript");
}
x();
```

In the above code, `Namaste JavaScript` is printed before `1`, which in turn is printed after 3 seconds of a lapse.

What `setTimeout` does is, first its callback function forms a closure. Meaning it remembers the reference to `i`. Wherever this function goes, it takes the reference of `i` along with it. What `setTimeout` does is, it takes this callback function and stores it in some place and attaches a timer to it, and the rest of the code proceeds. Once the timer runs out, the `setTimeout` places that callback function to the call stack and runs it.

Sample code:

```js
function x() {
  for (var i = 1; i <= 5; i++) {
    setTimeout(function () {
      console.log(i);
    }, i * 1000);
  }

  console.log("Namaste JavaScript");
}
x();
```

Sample output:

```
Namaste JavaScript
6
6
6
6
6
```

**[NOTE:** All the lines with `6` are printed after a delay of 1 second.**]**

This behavior was observed because of the closure.

A closure is like a function along with its lexical environment. So, even when a function is taken out from its original scope, if it's executed in some other scope, it still remembers its lexical environment. Meaning it can access those variables of its lexical scope.

So what happens is, when the `setTimeout` takes this function and stores it somewhere and attaches a timer, the function remembers the reference to `i`. _It remembers the reference, not the value._

So, when the above code is executed, all 5 copies of the function are pointing to the same reference of `i`.

Sample code:

```js
function x() {
  for (let i = 1; i <= 5; i++) {
    setTimeout(function () {
      console.log(i);
    }, i * 1000);
  }

  console.log("Namaste JavaScript");
}
x();
```

Sample output:

```
Namaste JavaScript
1
2
3
4
5
```

**[NOTE:** All the digits are printed after a lapse of 1 second.**]**

Now, this behavior is observed in the case of this code since we've used `let`. The reason being that `let` is block scoped, which means that for every iteration, every `i` is a new copy all together and each time the `setTimeout` function is called, its callback function has a new copy of `i` with it. It forms a closure with a new variable each time. Each time the function is called, it is referring to a different memory location.

But, there's a workaround that we can achieve this even by using `var`.

Sample code:

```js
function x() {
  for (var i = 1; i <= 5; i++) {
    function close(i) {
      setTimeout(function () {
        console.log(i);
      }, i * 1000);
    }
    close(i);
  }

  console.log("Namaste JavaScript");
}
```

So, _we've formed a closure_. We created a function `close` and enclosed the `setTimeout` within it. Also, we're passing the value of `i` to this function `close`. This works because every time we call this `close` function with this `i`, it creates a new copy of `i` for itself when we **pass by value**.

---

### More on Closures

Sample code:

```js
function outer() {
  var a = 10;
  function inner() {
    console.log(a);
  }
  return inner;
}
outer()();
```

Sample output:

```
10
```

In the last statement of the code we have `outer()();`. This statement actually executes the inner function. It is able to do so as per the syntax since invoking the `outer()` returns `inner` which we are in turn calling by chaining another pair of `()`.

One example of data hiding using closures would be the following:

```js
function counter() {
  var count = 0;
  return function incrementCounter() {
    count++;
    console.log(count);
  };
}
var counter1 = counter();
counter1();
```

If we try to access `count` outside the function `counter()`, we'll get a `ReferenceError` of it being `not defined`.

Sample code:

```js
function counter() {
  var count = 0;
  return function incrementCounter() {
    count++;
    console.log(count);
  };
}

var counter1 = counter();
counter1();
counter1();

var counter2 = counter();
counter2();
```

Sample output:

```
1
2
1
```

This behavior is observed since each time we call `counter`, we get a fresh reference of the function being returned.

A more preferred way of creating a `Counter` would be using a constructor function.

Sample code:

```js
function Counter() {
  var count = 0;
  this.incrementCounter = function () {
    count++;
    console.log(count);
  };
  this.decrementCounter = function () {
    count--;
    console.log(count);
  };
}
var counter1 = new Counter();

counter1.incrementCounter();
counter1.incrementCounter();
counter1.decrementCounter();
```

Sample output:

```
1
2
1
```

**A disadvantage of closures:**

There could be an over consumption of memory in closures. This happens since the references enclosed in closures are not garbage collected and if not handled properly, might lead to memory leaks.

**What is a garbage collector and what does it do?**

Garbage collector is like a program in the browser or in the JavaScript engine which frees up the un-utilized memory. In languages like **C** and **C++**, it's up to the developers to allocate and de-allocate memory, but in high level languages like JavaScript, the garbage collector frees up the memory by releasing space attached to data members which are not in use, meaning when they are no longer needed.

**Relationship between garbage collector and closures**

Sample code:

```js
function a() {
  var x = 0;
  return function b() {
    console.log(x);
  };
}
var y = a();
y();
```

- In the above code, `x` is enclosed with `b` and `b` is being returned and stored in `y`. 
- The means that the garbage collector is unable to release the memory allocated to `x`, 
- since the function stored in `y` can be invoked anywhere in the code,
-  which in turn has a dependency on the variable `x`.

- But in some modern browsers and engines, for instance V8 in Chrome, have smart garbage collection mechanisms where if it finds out that somehow this variable is unreachable then it smartly collects the garbage variables.
- For example, if we had another variable outside `b` and inside `a` alongside `x`, then once the function `b` was returned, then any variable other than `x` would be garbage collected in V8 of Chrome. 
- This happens since it's clear from the code that `b` has a dependency on only `x` for the moment being, and unless we use any other variable from `b`'s lexical parent, there's no other dependency on its lexical parent.

---