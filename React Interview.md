# React Interview
## Basic
### Differentiate between Real DOM and Virtual DOM.
![](https://i.imgur.com/grhUQL2.png)
> Virtual DOM updates faster than Real DOM and no memory waste. This will help to increase the speed.

> Virtual DOM only save abstract things instead of the whole CSS, files. Virtual DOM will compare the difference between with the latest rendered DOM, and only update the difference. This will also help to improve the performance.

### What are the advantages of using React?
>* It increases the application’s performance
>* It is easy to know how a component is rendered, you just need to look at the render function.
>* JSX makes it easy to read the code of your components. It is also really easy to see the layout, or how components are plugged/combined with each other.
>* It use server side rendering. This enables improves SEO and performance.
>* It is easy to test.
>* You can use React with any framework (Backbone.js, Angular.js) as it is only a view layer.

### What are the limitations of React?
> * React is just a library, not a full-blown framework
> * Its library is very large and takes time to understand
> * It can be little difficult for the novice programmers to understand
> * Coding gets complex as it uses inline templating and JSX

### What is JSX?
>JSX is a syntax extension to JavaScript and comes with the full power of JavaScript. This is a type of file used by React which utilizes the expressiveness of JavaScript along with HTML like template syntax.

>You can embed any JavaScript expression in JSX by wrapping it in curly braces. After compilation, JSX expressions become regular JavaScript objects. This means that you can use JSX inside of if statements and for loops, assign it to variables, accept it as arguments, and return it from functions.

### How Virtual DOM working? 
>React’s render function creates a node tree out of the React components. It then updates this tree when chages made, and only update the changes.

>1. Whenever any underlying data changes, the entire UI is re-rendered in Virtual DOM representation.
>2. Then the difference between the previous DOM representation and the new one is calculated.
>3. Once the calculations are done, the real DOM will be updated with only the things that have actually changed. 

###  How different is React’s ES6 syntax when compared to ES5?
>* require vs import

~~~ javascript
// ES5
var React = require('react');
 
// ES6
import React from 'react';
~~~
>* exports vs export

~~~ javascript
// ES5
module.exports = Component;
 
// ES6
export default Component;
~~~
>* component and function

~~~ javascript
// ES5
var MyComponent = React.createClass({
    
});
 
// ES6
class MyComponent extends React.Component {
    
} 
~~~
### How is React different from Angular?
![](https://i.imgur.com/BZvhcZB.png)

### Server-side rendering
>浏览器渲染单页应用用的基本都是浏览器渲染。优点很明确，后端只提供数据，前端做视图和交互逻辑，分工明确。服务器只提供接口，路由以及渲染都丢给前端，服务器计算压力变轻了。但是弱点就是用户等待时间变长了，尤其在请求数多而且有一定先后顺序的时候。

>服务器渲染服务器接到用户请求之后，计算出用户需要的数据，然后将数据更新成视图（也就是一串dom字符）发给客户端，客户端直接将这串字符塞进页面即可。这样做的好处是响应很快，用户体验会比较好，另外对于搜索引擎来说也是友好的，有SEO优化。现在题主说的应该是nodejs层的服务器渲染，这里还有一个明显的好处就是前端性能优化更顺手了，可操作的空间大了。但是缺点也很明显，如果不是增加一个node层的话，前后端责任分工不明，不能很好的并行开发。另外也增加了服务器计算压力（虽然可以做渲染缓存，但毕竟是多做了计算）。

>服务器端渲染可以让搜索引擎更容易读取页面的meta信息以及其他SEO相关信息，大大增加网站在搜索引擎中的可见度。

## Component
###  What do you understand from “In React, everything is a component.”
>Components are the building blocks of a React application’s UI. These components split up the entire UI into small independent and reusable pieces. Then it renders each of these components independent of each other without affecting the rest of the UI。

### What is the difference between a Presentational component and a Container component?
>Presentational components are concerned with how things look. They generally receive data and callbacks exclusively via props. These components rarely have their own state, but when they do it generally concerns UI state, as opposed to data state. 关注于该怎样展现，不关注数据是怎么加载和处理的，只通过props来获取数据和回掉函数

>Container components are more concerned with how things work. These components provide the data and behavior to presentational or other container components. They call Flux actions and provide these as callbacks to the presentational components. They are also often stateful as they serve as data sources. 关注与该怎么运行，由于他们经常作为数据来源的角色，所以container一般会包含state（包含其他组件）

### What are the differences between a class component and functional component?（？？？？？）
>* Class components allows you to use additional features such as local state and lifecycle hooks. Also, to enable your component to have direct access to your store and thus holds state.
>* When your component just receives props and renders them to the page, this is a 'stateless component', for which a pure function can be used. These are also called dumb components or presentational components.

### Differentiate between stateful and stateless components.
![](https://i.imgur.com/j4fJPMe.png)

### What do you know about controlled and uncontrolled components?
![](https://i.imgur.com/AUkRTdd.png)
> An input form element whose value is controlled by React in this way is called a "controlled component".

### Explain the purpose of render() in React.
>Each React component must have a render() mandatorily. It returns a single React element which is the representation of the native DOM component. If more than one HTML element needs to be rendered, then they must be grouped together inside one enclosing tag such as \<span>,\<div> etc.

### What is Props?
>Props is the shorthand for Properties in React. They are read-only components which is immutable. They are always passed down from the parent to the child components throughout the application. A child component can never send a prop back to the parent component. 
>
>This help in maintaining the unidirectional data flow and are generally used to render the dynamically generated data.

### What is a state in React and how is it used?
>States are the heart of React components. States are the source of data and must be kept as simple as possible. Basically, states are the objects which determine components rendering and behavior. They are mutable unlike the props and create dynamic and interactive components. They are accessed via this.state().

###  Differentiate between states and props.
![](https://i.imgur.com/gJsujC8.png)
>The state is a data structure that starts with a default value when a Component mounts. It may be mutated across time, mostly as a result of user events.

>Props are a Component's configuration. They are received from above and immutable as far as the Component receiving them is concerned. A Component cannot change its props, but it is responsible for putting together the props of its child Components. Props do not have to just be data - callback functions may be passed in as props.

###  How can you update the state of a component?
> use `setState()` to update the state, there are two ways to use setState: anonymous function and object.
> 
> When the update is relay on the state, and you want to make changes on the state, you need to use anonymous function. Using Object way will change all the state.

### What is arrow function in React? How is it used?
> Arrow functions are more of brief syntax for writing the function expression. These functions allow to bind the context of the components properly since in ES6 auto binding is not available by default. This is an alternative way of binding `this`. 
> 
> Arrow functions are easy to read and write, and scopt safty.

### What are the different phases of React component’s lifecycle?
> 1. `Initial Rendering Phase`: This is the phase when the component is about to start its life journey and make its way to the DOM.
> 2. `Updating Phase`: Once the component gets added to the DOM, it can potentially update and re-render only when a prop or state change occurs. 
> 3. `Unmounting Phase`: This is the final phase of a component’s life cycle in which the component is destroyed and removed from the DOM.

### Explain the lifecycle methods of React components in detail.
>* `componentWillMount()` – App configuration, executed just before rendering  the client and server-side.
>* `componentDidMount()` – Here you do all the setup you couldn’t do without a DOM. Executed on the client side only after the first render.
>* `componentWillReceiveProps()` – Invoked as soon as the props are received from the parent class and before another render is called.
>* `shouldComponentUpdate()` – Returns true or false value based on certain conditions. If you want your component to update, return true else return false. By default, it returns false. This prevent a rerender if component receives new prop
>* `componentWillUpdate()` – Called just before rendering takes place in the DOM.
>* `componentDidUpdate()` – Called immediately after rendering takes place. Commonly used to update the DOM in response to prop or state changes.
>* `componentWillUnmount()` – You can cancel any outgoing network requests, or remove all event listeners associated with the component. It is used to clear up the memory spaces.

### Where in a React component should you make an AJAX request?
> `componentDidMount` is where an AJAX request should be made in a React component. This method will be executed when the component “mounts” (is added to the DOM) for the first time. This method is only executed once during the component’s life.

### What is an event in React?
> In React, events are the triggered reactions to specific actions like mouse hover, mouse click, key press, etc. Handling these events are similar to handling events in DOM elements. But there are some syntactical differences like: 
> 
> * Events are named using camel case instead of just using the lowercase.
> * Events are passed as functions instead of strings.
> 
> The event argument contains a set of properties, which are specific to an event. Each event type contains its own properties and behavior which can be accessed via its event handler only.

### What are synthetic events in React?（？？？）
> Synthetic events are the objects which act as a cross-browser wrapper around the browser’s native event. They combine the behavior of different browsers into one API. This is done to make sure that the events show consistent properties across different browsers.

### What do you understand by refs in React?(25????)
> Refs is the short hand for References in React. It is an attribute which helps to store a reference to a particular React element or component, which will be returned by the components render configuration function. It is used to return references to a particular element or component returned by render(). They come in handy when we need DOM measurements or to add methods to the components.

~~~ javascript
class ReferenceDemo extends React.Component{
     display() {
         const name = this.inputDemo.value;
         document.getElementById('disp').innerHTML = name;
     }
render() {
    return(        
         <div>
            Name: <input type="text" ref={input => this.inputDemo = input} />
            <button name="Click" onClick={this.display}>Click</button>            
            <h2>Hello <span id="disp"></span> !!!</h2>
        </div>
    );
   }
 }
~~~
Refs are used to get reference to a DOM node or an instance of a component in React. Good examples of when to use refs are for managing focus/text selection, triggering imperative animations, or integrating with third-party DOM libraries. You should avoid using string refs and inline ref callbacks. Callback refs are advised by React.

###  List some of the cases when you should use Refs.(26????)
> When you need to manage focus, select text or media playback
> 
> To trigger imperative animations
>
>Integrate with third-party DOM libraries

### How are forms created in React?
~~~javascript
handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
}
 
render() {
    return (        
        <form onSubmit={this.handleSubmit}>
            <label>
                Name:
                <input type="text" value={this.state.value} onChange={this.handleSubmit} />
            </label>
            <input type="submit" value="Submit" />
        </form>
    );
}
~~~

### How would you prevent a component from rendering?
> Returning null from a component's render method does not affect the firing of the component's lifecycle methods.

### What is the purpose of super(props)?
> A child class constructor cannot make use of this until super() has been called. Also, ES2015 class constructors have to call super() if they are subclasses. The reason for passing props to super() is to enable you to access this.props in the constructor.

## Redux
### What is Redux?
> Redux is one of the hottest libraries for front-end development. It is used for the state management.
> 
> The basic idea of redux is that the entire application state is kept in a single store. The store is simply a javascript object. The only way to change the state is by firing actions from your application and then writing reducers for these actions that modify the state. 

### List down the components of Redux.
> **Action** – It’s an object that describes what happened.
> 
> * In the Object there should indicate the type of action. In essence, actions are payloads of information that send data from your application to your store.
> 
> **Reducer** –  Reducers are pure functions which specify how the application’s state changes in response to an ACTION. It also provide the the initial state to store and watch for the changes. 
> 
> * Reducers work by taking in the previous state and action, and then it returns a new state. It determines what sort of update needs to be done based on the type of the action, and then returns new values. It returns the previous state as it is, if no work needs to be done.
> 
> **Store** – It is a javascript object that holds application state. It has three responsibilities: 
> 
> * Allows access to state via getState()
> * Allows state to be updated via dispatch(action)
> * Registers listeners via subscribe(listener)
> 
> **View** – Simply displays the data provided by the Store.

### What is Redux Thunk used for?
> Redux thunk is middleware that allows you to write action creators that return a function instead of an action. The thunk can then be used to delay the dispatch of an action if a certain condition is met. This allows you to handle the asyncronous dispatching of actions.

### What are the advantages of Redux?
> **Predictability of outcome** – Since there is always one source of truth, i.e. the store, there is no confusion about how to sync the current state with actions and other parts of the application.
> 
> **Maintainability** – The code becomes easier to maintain with a predictable outcome and strict structure.
> 
> **Server-side rendering** – You just need to pass the store created on the server, to the client side. This is very useful for initial render and provides a better user experience as it optimizes the application performance.
> 
> **Developer tools** – From actions to state changes, developers can track everything going on in the application in real time.
> 
> **Community and ecosystem** – Redux has a huge community behind it which makes it even more captivating to use. A large community of talented individuals contribute to the betterment of the library and develop various applications with it.
> 
> **Ease of testing** – Redux’s code is mostly functions which are small, pure and isolated. This makes the code testable and independent.
> 
> **Organization** – Redux is precise about how code should be organized, this makes the code more consistent and easier when a team works with it.

## React Router
### What is React Router?
> React Router is a powerful routing library built on top of React, which helps in adding new screens and flows to the application. This keeps the URL in sync with data that’s being displayed on the web page. It maintains a standardized structure and behavior and is used for developing single page web applications. React Router has a simple API.

### Why is switch keyword used in React Router v4?
> The ‘switch’ keyword is used when you want to display only a single route to be rendered amongst the several defined routes. The <switch> tag when in use matches the typed URL with the defined routes in sequential order. When the first match is found, it renders the specified route. Thereby bypassing the remaining routes.

### Why do we need a Router in React?
> A Router is used to define multiple routes and when a user types a specific URL, if this URL matches the path of any ‘route’ defined inside the router, then the user is redirected to that particular route. So basically, we need to add a Router library to our app that allows creating multiple routes with each leading to us a unique view.

###  List down the advantages of React Router.
> Just like how React is based on components, in React Router v4, the API is ‘All About Components’. A Router can be visualized as a single root component (<BrowserRouter>) in which we enclose the specific child routes (<route>).
> 
> No need to manually set History value: In React Router v4, all we need to do is wrap our routes within the <BrowserRouter> component.
> 
> The packages are split: Three packages one each for Web, Native and Core. This supports the compact size of our application. It is easy to switch over based on similar coding style.



