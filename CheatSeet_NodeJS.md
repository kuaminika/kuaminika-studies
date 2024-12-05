# The Node JS cheat sheet

The following contains Key notes about Node JS

## Node JS is

- It's a an open  open-source cross platform runtime environment that allows you to execute JS code server side. Not just on the browser.
- It was created by Ryan Dahl in 2009
- It's useful to build:
  - Web applications
  - Web API
  - real time applications
  - CMS.
  - Server less functions

## Difference between  Browser JS and Node JS

| |Browser JS | NodeJS |
|--|--|--|
|Manipulation| you manipulate the DOM object| you manipulate Domain logic, Backend logic |
|Environment|Front end| Back end|
|Where code resides|browser|Server|

## How to install node JS

Instructions can be found here: [https://nodejs.org/en](https://nodejs.org/en)

## Event loop and concurrency

More is discussed in [here](/javascript_cheatsheet.md#event-loop-and-concurrency)

### SetImmediate and NextTick

The setImmediate() and nextTick() functions in Node.js are both used to schedule callbacks to be executed after the current operation completes.

- _nextTikck_ runs at the beginning of the next tick of the loop.
- setImmediate runs at the end of the event loop.

- In the code below

  ```js
   const {  setImmediate } = require('timers/promises');
 
    const {nextTick} = process;

      console.log('Start');

      setImmediate(() => {
        console.log('setImmediate');
      });

      nextTick(() => {
        console.log('nextTick');
      });
      nextTick(() => {
        console.log('nextTick2');
      });


      setTimeout(() => {
        console.log('setTimeout');
      }, 0);

      console.log('End');

  ```

  - The output would be:
  
     Start
     End
     nextTick
     setTimeout
     setImmediate

## async await




## Important Node modules

||Module| utility|
|--|--|--|
|1|FS|file system module that allows you to read and write files in the server|
|2|Path|to manipulate paths|
|3|HTTP| to help create HTTP servers. Useful for creating APIs|
|4|OS| Provides an  abstraction of the OS and the CPU|
|5|Events|for event based programming|
|6|WS|Web socket module to implement websockets|


Note: the http module works with the event module


## Nodemon

It's a package used for live server rebuilds whenever there's a change in the code.

## NPM

It's an accronym for the Node Package Manager. It is used for installing packages inside of your code

## package.json

It's a file used to manage packages that your application depends on.
It helps manage:

1. Dependency management
1. Version maanagement
1. project meta data
1. script management
1. Configuration options.

you create it using the following command

```bash
 npm init 
```

## Express js

- It is a node JS framework that wraps the http module.

- you'd install express with the following npm command

```bash
  npm i express
```

### CRUD methods

- It is helpful for defining CRUD operations. Here's an example:

```javascript

  const express = require("express"); // to import the installed package insid your script

  const app = express(); // the express function is used to define an  app 


   app.post("/user",function(request,response){

        const user = request.body;

        // you then do some logic with the provided user

        response.status(200).json({message:"user is treated"});

   });
```

In the above example, app.post uses the post HTTP method to implement the CREATE method in CRUD.

- The app.post method has two parameters.
   1. the Express route (i.e the path at which the middleware logic is executed)
   1. the call back function containing the respective middleware logic.

### Express router

you'd use the router like this:

```js
   const express = require("express");
   const  router = express.router()
```

## Mongo DB

- It's a document oriented NoSQL database.

- The following command to install mongo db

```bash
  npm i mongodb
```

Mongoose is a wrapper to mongo DB.

### Comparing SQL and No SQL

|SQL|No SQL|
|--|--|
|tables|collections|
|rows|documents|
|columns|keys an values|

