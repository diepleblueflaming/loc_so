							// IMPORTANT JS CONCEPT

/***********************************************/ 
Blocks in JavaScript do not create a new scope, 
so variables should be defined at the top of the function, not in blocks.
/************************************************/ 

/***********************************************/ 
 When a function gets declared, it contains a function definition and a closure. 
 The closure is a collection of all the variables in scope at the time of creation of the function.
/************************************************/ 

/******************** Object ***************************/ 
1. All objects created from object literals are linked to Object.prototype.

2. The prototype relationship is a dynamic relationship. 
 If we add a new property to a prototype, that property will immediately be visible in all of the objects that are based on that prototype.

3. hasOwnProperty does not look at the prototype chain

4. function -> Function.prototype -> Object.prototype

5. All argumnets will be defined as variables in the function. 
Unlike ordinary variables, instead of being initialized to undefined , 
they will be initialized to the arguments supplied when the function is invoked

6. Argument is not an real array. it like array object: has length property but lack all method 
 To convert arguments to array using: Array.from(arguments)
/************************************************/ 

Synchronous JavaScript: every statement of the code gets executed one by one. So, basically a statement has to wait for the earlier statement to get executed.
Asynchronous: mean that a statement after asynchronous code can be run immediately without waiting.

	/** JS EVENT LOPP, CALLSTACK, EVENT TABLE, CALLBACK QUEUE, JOB/EVENT QUEUE, HAEP **/

7. Call Stack
 - Where all javascript code gets pushed in and executed one by one and and gets popped out once the execution is done.
 
 //NOTE : 
  - All synchronous code directly get pushed into callstack.
  - All asynchronous code will be forwarded to [EVENT TABLE](setTimeout, ajax, promise, element event).
  - Code in Promise function is synchronous code.

8. EVENT TABLE
- Event table responsible for moving all asynchronous code to callback/event queue after specified time.  
  
9. HEAP
- HEAP is where memory allocation happens for all variable that is defined in program.

10. Callback queue (Include Task Queue(also know as Macro Task) and Job Queue(Micro Task))
- Callback queue is where all asynchronous code gets pushed to and wait for the execution.

11.Task Queue
- Task Queue where asynchronous code like: callback of an event, callback in setTimeout, setInterval, code from a console or <script> tag gets pushed to.
 + A new JavaScript program or subprogram is executed (such as from a console, or by running the code in a <script> element) directly.
 + An event fires, adding the event's callback function to the task queue.
 + A timeout or interval created with setTimeout() or setInterval() is reached, causing the corresponding callback to be added to the task queue.
 
- Job Queue is where all codes in thenable method(callback method) of a Promise are added to once when Promise is resolved.
- Job Queue have priority than Task Queue.

12. Event Loop 
 - Event loop keeps running continuously and check Call Stack.
 There are two case: 
 - If Call Stack is not empty(has any statement to execute) then it will not check the callback queue.
 - If Call Stack is empty, it will check the Callack Queue(both [Task Queue] and [Job Queue]).
  + First it will check Job Queue and then check Task Queue.
   If [Callback Queue] not empty it will take first event from [Calback Queue] and push it to [Call Stack] to execution.
   
   
	/** JS SET TIMEOUT, SET INTERVAL **/

13. setTimeout
- Allows us run a function once after specific delay milliseconds.
- setTimeout return a "timmer identifier".
- To cancel the execution of setTimout/setInterval we should call clearTimeout with the "timmer identifier" returned from setTimeout.
- Zero delay scheduling with setTimeout(func, 0) (the same as setTimeout(func)) is used to schedule the call “as soon as possible, but after the current script is complete”.
- If we ommit the second paramater or pass a negative number, the value "0" will be used.

14. setInterval
- Allow us to run a function regular after specific delay times.
- setInterval return a "timmer identifier".
- To cancel the execution of setInterval we should call clearInterval with the "timmer identifier" returned from clearInterval.
- Zero delay scheduling with setInterval(func, 0) is used to schedule the call “as soon as possible, but after the current script is complete”.
- If we ommit the second paramater or pass a negative number, the value "0" will be used.
   
   
     /* Promise */
- A promise is an object that may produce a single value some time in the future

- A promise is my be in one of three posible state:
 + pending - when create new promise and not yet fullfiled or rejected.
 + Fullfiled - when resove() was called.
 + Rejected - when reject was called.
 
- A promise is settled if it is not pending.

- When a promise is settled it can not be resettled. Calling resolve() or reject() again will have no effect.

- Every promise must supply a [.then()] method and [.then()] method may be called many time on the same promise.

- Then method have two optional funtion are: onFullfilled and onRejected
 + onFullilled: will be called when promise fullfilled
 + onRejected: will be called when promise is rejected
 
- We can use the [.catch ()] method to handle the error occurring in [handleSuccess] of the then method.

- There are 6 userful method in Promise class:
 + Promise.reject() returns a rejected promise.
 
 + Promise.resolve() returns a resolved promise.
 
 + Promise.race() takes an array (or any iterable) and returns a promise that resolves with the value of the first resolved promise in the iterable,
   or rejects with the reason of the first promise that rejects.
   
 + Promise.all() takes an array (or any iterable) and returns a promise that resolves when all of the promises in the iterable argument have resolved,
   or rejects with the reason of the first passed promise that rejects.
   
 + Promise.allSettled() method returns a promise that resolves after all of the given promises have either fulfilled or rejected,
   with an array of objects that each describes the outcome of each promise.  
 
 + Promise.any() takes an iterable of Promise objects and, as soon as one of the promises in the iterable fulfills,
   returns a single promise that resolves with the value from that promise.
   If no promises in the iterable fulfill (if all of the given promises are rejected), then the returned promise is rejected with an AggregateError
   
   
  /** aysnc and await **/

- The async keyword before a function has two effects:
 + Makes it always return a promise.
 + Allows await to be used in it.

- The await keyword before a promise makes JavaScript wait until that promise settles, and then:
 + If it’s an error, the exception is generated — same as if throw error were called at that very place.
 + Otherwise, it returns the result.
 
 
  /** Closure **/

- A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment).
  In other words, a closure gives you access to an outer function’s scope from an inner function even outer funtion has finished.
  In JavaScript, closures are created every time a function is created, at function creation time.
- All funtion in JS is closure



 /** Scope **/
 
 - Global Scope: There is only one Global Scope in a Javascript Document i.e. area outside all the functions and how you can identify a global scope is that the variable defined in the global scope can be accessed anywhere in the code.

- Local Scope: Variables declared inside functions are local to the function and is bound to the corresponding local scope.
  Those variables cannot be accessed outside the functions.
  The local scope can be further divided into function scope and block scope.   
  + Function scope is within the function.
  + Block scope is within curly brackets.

- Lexical Scoping defines how variable names are resolved in nested functions: inner functions contain the scope of outer functions.


 /** var, let, const **/

 - var declarations are globally scoped or function scoped while let and const are block scoped.
 - var variables can be updated and re-declared within its scope; let variables can be updated but not re-declared; const variables can neither be updated nor re-declared.
 - They are all hoisted to the top of their scope. But while var variables are initialized with undefined
   let and const variables are not initialized.
    + Meaning: The block of code is aware of the variable, but it cannot be used until it has been declared.
    + Using a let or const variable before it is declared will result in a ReferenceError.
    + The variable is in a "temporal dead zone" from the start of the block until it is declared.
    
 - While var and let can be declared without being initialized, const must be initialized during declaration.
 - let and const does not create properties of the window object when declared globally (in the top-most scope).
 
 
	/** Hoisting **/
- Hoisting is JavaScript's default behavior of moving all declarations to the top of the current scope 

   
	/** JS coercion **/
- Type coercion is the process of converting value from one type to another when compared.


	/** Function Statement and function expresstion */

- function statement
 + are hoisted so you can using it anywhere in scope that defined it.
 + it must have name

- function expresstion
 + are not hoisted so you can only use it after declared
 + The name may be omitted in function expressions

- IIFE (immediately invoked function expressions)
 + It is a JavaScript function that runs as soon as it is defined.
 + An Immediately Invoked Function Expression is a good way at protecting the scope of your function and the variables within it.
 
 
 	/** this keyword **/
- "this" is a property of an execution context.

- in the global execution context this refers to the global object whether in strict mode or not.
- Inside a function, the value of "this" depends on how the function is called.
- In an event, this refers to the element that received the event.
- arrow funtion have no this. When this is accessed inside an arrow function, it is taken from outside.


	/** bind, call, apply **/
	
- bind, call, apply functions are used to change value of “this” inside a function with given object.

- The bind method creates a new function and sets the this value to the specified object.
- bind not execute function immediately.

- The call method sets the this value inside the function with given value  and immediately executes that function.
- call() accepts a comma-separated list of arguments

- apply method is similar to call() method
- apply() method accepts an array as the argument.

- If the new value of “this” is not passed, the global object will be used.


	/** Spread and rest syntax **/
	
- Spread syntax "expands" an array into its elements
- Rest syntax collects multiple elements and "condenses" them into a single element.


	/** primity and references **/
	
- JavaScript provides six primitive types as undefined, null, boolean, number, string, and symbol , and a reference type object.	
- The size of a primitive value is fixed, therefore, JavaScript stores the primitive value on the stack.
- The size of a reference value is dynamic so JavaScript stores the reference value on the heap.


	/** localStorage and sessionStorage **/

- Web storage objects localStorage and sessionStorage allow to save key/value pairs in the browser.
 + web storage objects are not sent to server with each request
 + The server can’t manipulate storage objects via HTTP headers.
 + The storage is bound to the origin
 + Different protocols or subdomains infer different storage objects, they can’t access data from each other.

- The main features of localStorage are:
 + Shared between all tabs and windows from the same origin.
 + The data does not expire. It remains after the browser restart and even OS reboot. 
 
- The sessionStorage exists only within the current browser tab.
 + Another tab with the same page will have a different storage.
 + But it is shared between iframes in the same tab (assuming they come from the same origin).
 + The data survives page refresh, but not closing/opening the tab. 
 
 
 	/** Cookie and Session */
 	
- Cookies and Sessions are used to store information. 

- Cookies
 + Cookies are only stored on the client-side machine
 + Cookies are text files stored on the client computer and they are kept of use tracking purpose. Server script sends a set of cookies to the browser.
 + When the browser sends a request to the server, cookie is also sent
 
- Session
 + A session creates a file in a temporary directory on the server where registered session variables and their values are stored.
   This data will be available to all pages on the site during that visit.
 + A session ends when the user closes the browser or after leaving the site, the server will terminate the session after a predetermined period of time.
