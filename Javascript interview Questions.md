## Javascript interview Questions
### Explain event delegation（事件委托）
> Event delegation is a technique involving adding event listeners to a parent element instead of adding them to the descendant elements. The listener will fire whenever the event is triggered on the descendant elements due to event bubbling up the DOM. The benefits of this technique are:
> 
> * Memory footprint goes down because only one single handler is needed on the parent element, rather than having to attach event handlers on each descendant.
> * There is no need to unbind the handler from elements that are removed and to bind the event for new elements.

### Explain how `this` works in JavaScript
> A hand-wavey explanation is that the value of `this` depends on how the function is called. 
> 
> 1. If the new keyword is used when calling the function, this inside the function is a brand new object.
> 2. If `apply`, `call`, or `bind` are used to call/create a function, `this` inside the function is the object that is passed in as the argument.
> 3. If a function is called as a method, such as `obj.method()` — `this` is bind with object `obj`. this 将绑定到obj对象。
> 4. If a function is invoked without any of the conditions present above, this is the global object.
> 5. If multiple of the above rules apply, the rule that is higher wins and will set the `this` value.（上述规则，1 号最高，4 号最低）
> 6. If the function is an ES6 arrow function, it ignores all the rules above and receives the `this` value of its surrounding scope at the time it is created.（被设置为它被创建时的上下文）

### Explain how prototypal inheritance works
> All JavaScript objects have a `prototype` property, that is a reference to another object. When a property is accessed on an object and if the property is not found on that object, the JavaScript engine looks at the object's prototype, and the prototype's prototype and so on, until it finds the property defined on one of the prototypes or until it reaches the end of the prototype chain.

### What do you think of AMD vs CommonJS?
>Then can be used to share code between files
>
> Both are ways to implement a module system, CommonJS is synchronous while AMD is asynchronous. CommonJS is closer to the style you would write import statements in other languages. Also, CommonJS syntax is closer to Node style of writing modules and there is less context-switching overhead when switching between client side and server side JavaScript development.

### Explain why the following doesn't work as an IIFE: `function foo(){ }();`. What needs to be changed to properly make it an IIFE?
> IIFE stands for Immediately Invoked Function Expressions. 立即执行函数
> 
> The JavaScript parser reads function `foo(){ }();` as `function foo(){ }` and `();`, where the former is a function declaration and the latter (a pair of brackets) is an attempt at calling a function but there is no name specified, hence it throws `Uncaught SyntaxError: Unexpected token )`.
> 
> Here are two ways to fix it that involves adding more brackets: `(function foo(){ })()` and `(function foo(){ }())`. 

### What's the difference between a variable that is: null, undefined or undeclared? How would you go about checking for any of these states?
> **Undeclared** variables are created when you assign a value to an identifier that is not previously created using var, let or const. Undeclared variables will be defined globally, outside of the current scope. In strict mode, a `ReferenceError` will be thrown when you try to assign to an undeclared variable. To check for them, wrap its usage in a `try/catch` block.
> 
> ~~~javascript
> function foo() {
>  x = 1; // Throws a ReferenceError in strict mode
> }
> 
> foo();
> console.log(x); // 1
> ~~~
> **Undefined** variable is a variable that has been declared, but not assigned a value. It is of type undefined. If a function does not return any value as the result, the variable also has the value of undefined. To check for it, compare using the strict equality (`===`) operator or `typeof` which will give the 'undefined' string. Note that you should not be using the abstract equality  operator (`==`) to check, as it will also return true if the value is null.
> 
> ~~~ javascript
> var foo;
> console.log(foo); // undefined
> console.log(foo === undefined); // true
> console.log(typeof foo === 'undefined'); // true
> 
> console.log(foo == null); // true. Wrong, don't use this to check!
> 
> function bar() {}
> var baz = bar();
> console.log(baz); // undefined
> ~~~
> A variable that is **null** will have been explicitly assigned to the null value. It represents no value and is different from undefined in the sense that it has been explicitly assigned. To check for null, simply compare using the strict equality operator. Note that like the above, you should not be using the abstract equality operator (==) to check, as it will also return true if the value is undefined.
> 
> ~~~ javascript
> var foo = null;
> console.log(foo === null); // true
>
> console.log(foo == undefined); // true. Wrong, don't use this to check!
> ~~~

### What is a closure, and how/why would you use one? 闭包
> A closure is the combination of a funct Closures are functions that have access to the outer (enclosing) function's variables—scope chain even after the outer function has returned. 闭包是即使被外部函数返回，依然可以访问到外部（封闭）函数作用域的函数。
> 
> ~~~ javascript
> function makeFunc() {
>    var name = "Mozilla";
>    function displayName() {
>        alert(name);
>    }
>    return displayName;
>}
>
>var myFunc = makeFunc();
>myFunc();
>~~~
>JavaScript中的函数会形成闭包。 闭包是由函数以及创建该函数的词法环境组合而成。这个环境包含了这个闭包创建时所能访问的所有局部变量。在我们的例子中，myFunc 是执行 makeFunc 时创建的 displayName 函数实例的引用，而 displayName 实例仍可访问其词法作用域中的变量，即可以访问到 name 。由此，当 myFunc 被调用时，name 仍可被访问，其值 Mozilla 就被传递到alert中。
>
> Why would you use one?
> 
> * they let you associate some data (the lexical environment) with a function that operates on that data.
> * Data privacy / emulating private methods with closures. Commonly used in the module pattern.
> * Partial applications or currying.

### Can you describe the main difference between a `.forEach` loop and a `.map()` loop and why you would pick one versus the other?
> `forEach`
> 
> * Iterates through the elements in an array.
> * Executes a callback for each element.
> * Does not return a value.
> 
> ~~~ javascript
> const a = [1, 2, 3];
>const doubled = a.forEach((num, index) => {
>  // Do something with num and/or index.
>});
>
>// doubled = undefined
>~~~
>`map`
>
> * Iterates through the elements in an array.
> * "Maps" each element to a new element by calling the function on each element, creating a new array as a result.
> 
>~~~ javascript
>const a = [1, 2, 3];
>const doubled = a.map(num => {
>  return num * 2;
>});
>
>// doubled = [2, 4, 6]
>~~~
>The main difference between `.forEach` and `.map()` is that `.map()` returns a new array. If you need the result, but do not wish to change the original array, `.map()` is the best choice. If you simply need to iterate over an array, `forEach` is a fine choice.

### What's a typical use case for anonymous functions?
> They can be used in **IIFEs** to encapsulate some code within a local scope so that variables declared in it **do not leak to the global scope**.
> 
> ~~~javascript
> (function() {
>  // Some code here.
>})();
>~~~
>**As a callback that is used once and does not need to be used anywhere else.**The code will seem more self-contained and readable when handlers are defined right inside the code calling them, rather than having to search elsewhere to find the function body.
>
> ~~~javascript
> setTimeout(function() {
>  console.log('Hello world!');
>}, 1000);
>~~~
>Arguments to functional programming constructs or Lodash (similar to callbacks). 函数式编程
>
>~~~javascript
>const arr = [1, 2, 3];
>const double = arr.map(function(el) {
>  return el * 2;
>});
>console.log(double); // [2, 4, 6]
>~~~

### How do you organize your code? (module pattern, classical inheritance?)
>  I use React/Redux which utilize a single-directional data flow based on Flux architecture. 单向函数编程
> 
> module pattern encourages a more OOP approach. The Object Oriented Approach

### What's the difference between host objects and native objects?
> Native objects are objects that are part of the JavaScript language, such as `String`, `Math`, `RegExp`, `Object`, `Function`, etc.
> 
> Host objects are provided by the runtime environment (browser or Node), such as `window`, `XMLHTTPRequest`, etc.

### Difference between: `function Person(){}`, `var person = Person()`, and `var person = new Person()`?
> `function Person(){}` is just a normal **function declaration**. 函数声明
> 
> `var person = Person()` **invokes the Person as a function**, and not as a constructor. 函数调用，不是声明。 Invoking as such is a common mistake. Typically, the constructor does not return anything, hence invoking the constructor like a normal function will return undefined.
> 
> `var person = new Person()` **creates an instance of the Person object** 创建函数 using the `new` operator, which inherits from `Person.prototype`. 
> 
> ~~~javascript
> function Person(name) {
>  this.name = name;
>}
>
>var person = Person('John');
>console.log(person); // undefined
>console.log(person.name); // Uncaught TypeError: Cannot read property 'name' of undefined
>
>var person = new Person('John');
>console.log(person); // Person { name: "John" }
>console.log(person.name); // "john"
>~~~

### What's the difference between .call and .apply?
> Both `.call` and `.apply` are used to invoke functions. However, `.call` takes in comma-separated arguments as the next arguments while `.apply` takes in an array of arguments as the next argument.
> 
> ~~~javascript
> function add(a, b) {
>  return a + b;
>}
>
>console.log(add.call(null, 1, 2)); // 3
>console.log(add.apply(null, [1, 2])); // 3
>//the first parameter is used as the value of this within the function
>~~~

### Explain `Function.prototype.bind`.
> It is most useful for binding the value of `this` in methods of classes that you want to pass into other functions. This is frequently done in React components.

### When would you use `document.write()`?
> `document.write()` writes a string of text to a document stream opened by `document.open()`. When `document.write()` is executed after the page has loaded, it will call `document.open` which clears the whole document (\<head> and \<body> removed!) and replaces the contents with the given parameter value. Hence it is usually considered dangerous and not recommended.

### Explain Ajax in as much detail as possible.
> Ajax (asynchronous JavaScript and XML) is a set of web development techniques to create asynchronous web applications. With Ajax, web applications can send data to and retrieve from a server asynchronously (in the background) without interfering with the display and behavior of the existing page. Ajax allow web pages to change content dynamically without the need to reload the entire page. Now use JSON together with Javascript, because it is native support.

### What are the advantages and disadvantages of using Ajax?
> Advantages:
> 
> * Better interactivity. New content from the server can be changed dynamically without the need to reload the entire page.
> * Reduce connections to the server since scripts and stylesheets only have to be requested once.
> * State can be maintained on a page. JavaScript variables and DOM state will persist because the main container page was not reloaded.
> 
> Disadvantages:
> 
> * Dynamic webpages are harder to bookmark.
> * Does not work if JavaScript has been disabled in the browser.
> * Some webcrawlers do not execute JavaScript and would not see content that has been loaded by JavaScript.

### Have you ever used JavaScript templating? If so, what libraries have you used?
> templating: JSX ( a syntax extension to JavaScript), closer to JavaScript
> 
> libraries: Angular, React

### Describe event bubbling.
> When an event triggers on a DOM element, it will attempt to handle the event if there is a listener attached, then the event is bubbled up to its parent. Event bubbling is the mechanism behind event delegation.

### What's the difference between an "attribute" and a "property"?
> Attribute: specified in HTML, always in the form of string
> 
> Property: specified in DOM object, can have any type of JavaScript

### Why is extending built-in JavaScript objects not a good idea?
>Extending a built-in/native JavaScript object means adding properties/functions to its prototype. Imagine your code uses a few libraries that both extend the Array.prototype by adding the same contains method, the implementations will overwrite each other and your code will break if the behavior of these two methods is not the same.

### Difference between document `load` event and document `DOMContentLoaded` event?
> The `DOMContentLoaded` event is fired when the initial HTML document has been completely loaded and parsed, without waiting for stylesheets, images, and subframes to finish loading.
> 
> window's `load` event is only fired after the DOM and all dependent resources and assets have loaded.

### What is the difference between `==` and `===`?
> `==` is the abstract equality operator while `===` is the strict equality operator. The `==` operator will compare for equality after doing any necessary type conversions. The `===` operator will not do type conversion, so if two values are not the same type `===` will simply return false. 

### Concat

>~~~javascript
> function duplicate(arr) {
>  return arr.concat(arr);
>}
>
>duplicate([1, 2, 3, 4, 5]); // [1,2,3,4,5,1,2,3,4,5]
>~~~
>Concat is a method to connect two or more array. It will not change the original array, but to return a copy of the array which it is connected to.

### Why is it called a Ternary expression, what does the word "Ternary" indicate? 三元
> "Ternary" indicates three, and a ternary expression accepts three operands, the test condition, the "then" expression and the "else" expression. 

### Create a for loop that iterates up to 100 while outputting "fizz" at multiples of 3, "buzz" at multiples of 5 and "fizzbuzz" at multiples of 3 and 5.
>~~~javascript
>for (var i=1; i <= 100; i++)
{
    if (i % 15 == 0)
        console.log("FizzBuzz");
    else if (i % 3 == 0)
        console.log("Fizz");
    else if (i % 5 == 0)
        console.log("Buzz");
    else
        console.log(i);
}
~~~

### Why is it not a good idea to leave the global scope?
> If everyone uses the global namespace to define their variables, collisions will likely occur. Use the module pattern (IIFEs) to encapsulate your variables within a local namespace.

### Explain what a single page app is and how to make one SEO-friendly. 搜索引擎优化
> Traditionally, the browser receives HTML from the server and renders it. When the user navigates to another URL, a full-page refresh is required and the server sends fresh new HTML to the new page. This is called server-side rendering.
> 
> However, in modern SPAs (single page application), client-side rendering is used instead. The browser loads the initial page from the server, along with the scripts (frameworks, libraries, app code) and stylesheets required for the whole app. When the user navigates to other pages, a page refresh is not triggered. The browser will retrive the new data from the server by sending AJSX requests. The SPA then dynamically updates the page with the data which has already downloaded in the initial page load. 
> 
> The benefits:
> 
> * The react speed is fast and users do not see the flash between page navigations due to full-page refreshes.
> * Fewer HTTP requests are made to the server, as the page has downloaded all asset when the page initial.
> * You can easily build new clients for different platforms (e.g. mobile, chatbots, smart watches) without having to modify the server code. 
> 
> the downsides:
> 
> * Heavier initial page load due to the loading of framework, app code, and assets required for multiple pages.
> * Needto configure to route all requests to a single entry point on your server and allow client-side routing to take over from there.

### What is the extent of your experience with Promises?
> A promise is an object that may produce a single value sometime in the future: either a resolved value or a reason that it's not resolved. A promise may be in one of 3 possible states: fulfilled, rejected, or pending. Promise users can attach callbacks to handle the fulfilled value or the reason for rejection. (添加回调函数来处理操作成功的结果或失败的原因。)

### What are the pros and cons of using Promises instead of callbacks?
> Pros:
> 
> * Avoid callback hell which can be unreadable.
> * Makes it easy to write sequential asynchronous code that is readable with `.then()`.
> * Makes it easy to write parallel asynchronous code with `Promise.all()`.
> 
> Cons:
> 
> * In older browsers where ES2015 is not supported, you need to load a polyfill in order to use it.

### What are some of the advantages/disadvantages of writing JavaScript code in a language that compiles to JavaScript?
> I have used Typescript.
> 
> * Fixes some of the longstanding problems in JavaScript and discourages JavaScript anti-patterns.
> * IDE/editor support might be lacking.
> * These languages will always be behind the latest JavaScript standard.

### What language constructions do you use for iterating over object properties and array items?
> For objects:
> 
> * `for` loops - `for (var property in obj) { console.log(property); }`. However, this will also iterate through its inherited properties, and you will add an `obj.hasOwnProperty(property)` check before using it.
> * `Object.keys()` - `Object.keys(obj).forEach(function (property) { ... })`.
> * `Object.getOwnPropertyNames()` - `Object.getOwnPropertyNames(obj).forEach(function (property) { ... })`.
> 
> For arrays: 
> 
> * `for` loops：`for (let i = 0; i < arr.length; i++)`. (ES6)
> * `forEach` - `arr.forEach(function (el, index) { ... })`.

### Explain the difference between synchronous and asynchronous functions.
> Synchronous functions are blocking while asynchronous functions are not.
> 
> In synchronous functions, statements complete before the next statement is run. In this case, the program is evaluated exactly in order of the statements and execution of the program is paused if one of the statements take a very long time.
> 
> Asynchronous functions usually accept a callback as a parameter and execution continue on the next line immediately after the asynchronous function is invoked. The main thread can continue executing other operations instead of blocking until that long operation to complete.

### What are the differences between variables created using let, var or const?
> Variables declared using the `var` keyword are scoped to the function in which they are created, or if created outside of any function, to the global object. `let` and `const` are block scoped, meaning they are only accessible within the nearest set of curly braces (function, if-else block, or for-loop).
> 
> `var` can be referenced in code before they are declared. `let` and `const` will not allow this, instead throwing an error.
> 
> ~~~javascript
> console.log(foo); // undefined
>
>var foo = 'foo';
>
>console.log(baz); // ReferenceError: can't access lexical declaration 'baz' before initialization
>
>let baz = 'baz';
>
>console.log(bar); // ReferenceError: can't access lexical declaration 'bar' before initialization
>
>const bar = 'bar';
>~~~
>Redeclaring a variable with `var` will not throw an error, but `let` and `const` will. 重复声明变量
>
> ~~~javascript
> var foo = 'foo';
>var foo = 'bar';
>console.log(foo); // "bar"
>
>let baz = 'baz';
>let baz = 'qux'; // Uncaught SyntaxError: Identifier 'baz' has already been declared
>~~~
>different between `let` and `const`: `let` allows assign value several times while `const` does not.
>
> ~~~javascript
> // This is fine.
>let foo = 'foo';
>foo = 'bar';
>
>// This causes an exception.
>const baz = 'baz';
>baz = 'qux';
>~~~

### What are the differences between ES6 class and ES5 function constructors?
> ~~~javascript
> // ES5 Function Constructor
>function Person(name) {
>  this.name = name;
>}
>
>// ES6 Class
>class Person {
>  constructor(name) {
>    this.name = name;
>  }
>}
>~~~
>The main difference in the constructor comes when using inheritance.

### Can you offer a use case for the new arrow => function syntax? How does this new syntax differ from other functions?

### What advantage is there for using the arrow syntax for a method in a constructor?

### Can you give an example for destructuring an object or an array? 解构
> Destructuring is an expression available in ES6 to extract values of Objects or Arrays and place them into distinct variables.
> 
> Array destructuring
> 
> ~~~javascript
> // Variable assignment.
>const foo = ['one', 'two', 'three'];
>
>const [one, two, three] = foo;
>console.log(one); // "one"
>console.log(two); // "two"
>console.log(three); // "three"
>~~~
>
>~~~javascript
>// Swapping variables
>let a = 1;
>let b = 3;
>
>[a, b] = [b, a];
>console.log(a); // 3
>console.log(b); // 1
>~~~
>Object destructuring
>
>~~~javascript
>// Variable assignment.
>const o = { p: 42, q: true };
>const { p, q } = o;
>
>console.log(p); // 42
>console.log(q); // true
>~~~

### ES6 Template Literals offer a lot of flexibility in generating strings, can you give an example? 模板字符串
>~~~javascript
>`string text``string text line 1
> string text line 2``string text ${expression} string text`;
>
>tag`string text ${expression} string text`;
>~~~

### How could you write a method on instance of a date which will give you next day?
>~~~javascript
>Date.prototype.nextDay = function(){
>  var currentDate = this.getDate();
>  return new Date(this.setDate(currentDate +1));
>}
>
>var date = new Date(); 
>date; //Fri May 16 2014 20:47:14 GMT-0500 (Central Daylight Time)
>date.nextDay();//Sat May 17 2014 20:47:14 GMT-0500 (Central Daylight Time)
>~~~

