# How JavaScript Works?

> Is JavaScript:
>
> - <i><mark>**Synchronous**</mark> or Asynchronous?</i>
> - <i><mark>**Single-threaded**</mark> or Multi-threaded?</i>
 ##  JavaScript is a synchronous, single-threaded language.
> ### 🧠 What does “JavaScript is synchronous and single-threaded” mean?
## 🔹 1. Single-threaded
- JavaScript has one main thread to execute code.

- That means it can only do one thing at a time.

- It uses a single Call Stack, and instructions are executed line by line, in the order they appear.

## 🔹 2. Synchronous
- In a synchronous language, tasks are executed sequentially, i.e., one after another.

- JavaScript waits for the current task to finish before moving to the next.

## ✅ So, if something takes a long time (e.g., a big loop), it will block the entire thread.
![Execution context](../images/execution-context.jpg)



# 🧠 What is an Execution Context?

- Everything in JavaScript happens inside an **Execution Context**
  - You can assume this _execution context_ to be a big box or a container in which the whole JavaScript code is executed.
  - This **big box** has two components in it:
    - **Memory creation:** This is the place where all variables and functions are stored as key-value pairs. This _'memory component'_ is also known as the **Variable Environment**. So, it's sort of an environment in which all these variables and functions are stored as key-value pairs.
    - **Code execution :** This is the place where the code is executed one line at a time. This _'code component'_ is also known as the **Thread of Execution**. So, this _thread of execution_ is just like a thread in which the whole code is executed one line at a time.
- JavaScript is a **_synchronous single-threaded_** language.
  - **Single-threaded** means that JavaScript can only execute one command at a time.
  - **Synchronous single-threaded** means that JavaScript can only execute one command at a time and in a specific order. That means that it can only go to the next line once the current line has finished executing. This is what it means by being **_synchronous single-threaded_**.