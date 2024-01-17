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
