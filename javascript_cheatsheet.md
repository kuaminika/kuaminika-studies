# Javascript cheat sheet

**Note**: there's react cheatsheet as well. [right here](/reactJS_cheatsheet.md)

## DOM stuff

### Nodelist

- It is not an array so it does not have map however it has a forEach().

## Intersection observer

- It's used for:
  - windowing
  - know when a div left a screen.
- arguments
  - callback
  - options:the options is object with key attriubutes such as :
    - root : the element that we're checking to be visible
    - threshold: how much of the target that we want to be visible
    - margin: (i.e rootMargin) it can be used to shorten the area of observation

## Event loop and concurrency

First of all, it is important to note that Node JS, or JS for that matter is NOT multi-threaded.

- It uses the **event loop** which is a mechanism in Javascript that handles asynchronous operations.
  - It allows for the js engine to execute other tasks  while waiting for asynchronous operations.
- The _Javascript engine_ executes js line by line.
- The  _call stack_ stores function calls
- In browser JS, there are 3 synchronous queues
  1. Macro Task queue
  1. micro task queue
  1. animation queue 


## call back hell