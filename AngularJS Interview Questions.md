## AngularJS Interview Questions
### What is AngularJS?
> AngularJS is an open-source JavaScript framework designed for creating dynamic single web page applications with fewer lines of code. It help to build large scale and high performance web application.

### What is data binding in AngularJS and What is the difference between one-way and two-way binding?
> Data binding is the automatic synchronization of data between model and view components.AngularJS uses two-way data binding.
> 
> In one-way binding, view (UI part) not updates automatically when data model changed. We need to write custom code to make it updated every time.
> 
> In two-way binding, the scope variable changes its value every time its model binds to a different value. 

### What is scope in AngularJS?
> Scopes are objects that refer to the model. They act as glue between controller and view. Scopes are arranged in hierarchical structure which mimic the DOM structure of the application. Scopes can watch expressions and propagate events. 

### Explain the concept of scope hierarchy.
>Each AngularJS application has only one root scope. If we define nested controller, child controllers, however, create a scope for each view. When the new scopes are created, they are added to their parent root scope as child scopes. This creates a hierarchical structure when they are attached.  

### What are the controllers in AngularJS?
> Controllers are JavaScript functions that are bound to a particular scope which provide data and logic to HTML UI. They are the prime actors in AngularJS framework and carry functions to operate on data and decide which view is to be updated to show the updated model based data.

### How do you share data between controllers in AngularJs?
> We can share data by creating a service. Services are easiest, fastest and cleaner way to share data between controllers in AngularJs.
> 
>There are also other ways to share data between controllers, they are:
>
> * using `$event`
> * `$parent`, `nextSibling`, `controllerAs`
> * Using the `$rootScope`

### What are the services in AngularJS?
> AngularJS Services are objects that provide separation of concerns to an AngularJS app. These can be created using a factory method, provider method or a service method.
> 
> AngularJS come with several built-in services. For example $https: service is used to make XMLHttpRequests (Ajax calls). Services are singleton objects which are instantiated only once in app.

### What are the filters in AngularJS?
> Filters select a subset of items from an array and return a new array. Filters are used to show filtered items from a list of items based on defined criteria.

### Explain directives in AngularJS.
> Directives are markers on DOM elements (such as elements, attributes, css, and more). These can be used to create custom HTML tags that serve as new, custom widgets. AngularJS has built-in directives (ng-app, ng-bind, ng-model, etc) to perform most of the task that developers have to do.
> 
> * ng-app:- directive is used to flag the HTML element that Angular should consider to be the root element of our application.
> * ng-model:- directive allows us to bind values of HTML controls (input, select, textarea) to application data.This is two-way data binding. When using ngModel, not only change in the scope reflected in the view, but changes in the view are reflected back into the scope.
> * ng-bind:- directive binds application modal data to the HTML view.

### Explain templates in AngularJS.
> Templates are the rendered view with information from the controller and model. These can be a single file (like index.html) or multiple views in one page using "partials".
> 
> The template is the HTML portion of the angular app. It is exactly like a static HTML page, except that templates contain additional syntax which allows data to be injected in it in order to provide a customized user experience.

### What is routing in AngularJS?
> It is concept of switching views. AngularJS based controller decides which view to render based on the business logic.

### How to implement routing in AngularJS?
> 1. Add the “Angular-route.js” file to your view.
> 2. Inject “ngroute” functionality while creating Angular app object.
> 3. Configure the route provider. `$routerProvider` `.when()`
> 4. Define hyperlinks.
> 5. Define sections where to load the view. `ng-view`

### What is deep linking in AngularJS?
> Deep linking allows you to encode the state of application in the URL so that it can be bookmarked. The application can then be restored from the URL to the same state.

### What are the advantages of AngularJS?
> AngularJS provides capability to create Single Page Application in a very clean and maintainable way.

> AngularJS provides two way data binding capability to HTML thus giving user a rich and responsive experience.

> AngularJS code is unit testable.

> AngularJS uses dependency injection and make use of separation of concerns.

> AngularJS provides reusable components.

> Support static template and angular template。
> 
> Can add custom directive
> 
> Support both client and server communication

### What are the disadvantages of AngularJS?
> **Not Secure** − Being JavaScript only framework, application written in AngularJS are not safe. Server side authentication and authorization is must to keep an application secure.

> **Not degradable** − If your application user disables JavaScript then user will just see the basic page and nothing more.

### Which are the core directives of AngularJS?
> **ng-app** − This directive defines and links an AngularJS application to HTML. This is the start of the application and initial the application.

> **ng-model** − This directive binds the values of AngularJS application data to HTML input controls. It creates a model variable which can be used with the html page and within the container control having ng-app directive.

> **ng-bind** − This directive binds the AngularJS Application data to HTML tags.

### Explain AngularJS boot process.
> 1. HTML evaluate first, after JS is loaded, created angular global object. Then execute controller function.
> 2. Scan through HTML to look for AngularJS apps and views. Once view is located, it connects that view to corresponding controller function.
> 3. AngularJS executes the controller functions. It then renders the views with data from the model populated by the controller. The page gets ready.

### What is MVC?
> A Model View Controller pattern is made up of the following three parts:
> 
> * Model − It is the lowest level of the pattern responsible for maintaining data. 
> * View − It is responsible for displaying all or a portion of the data to the user.
> * Controller − It is a software Code that controls the interactions between the Model and View.

### Explain ng-controller directive.
> Attaches a controller class to view.
> 
> AngularJS application mainly relies on controllers to control the flow of data in the application. A controller is a JavaScript object containing attributes/properties and functions. Each controller accepts $scope as a parameter which refers to the application/module that controller is to control.

### Explain ng-init directive.
> ng-init directive initializes an AngularJS Application data. It is used to put values to the variables to be used in the application.

### Explain ng-repeat directive.
> ng-repeat directive repeats html elements for each item in a collection.

### What are AngularJS expressions?
> Expressions are used to bind application data to html. Expressions are written inside double braces like {{ expression}}. Expressions behave in same way as ng-bind directives. AngularJS application expressions are pure JavaScript expressions and outputs the data where they are used.

### Explain filter filter.
> filter filter is used to filter the array to a subset of it based on provided criteria.
> 
~~~ javascript
Enter subject: <input type = "text" ng-model = "subjectName">
Subject:
<ul>
  <li ng-repeat = "subject in student.subjects | filter: subjectName">
    {{ subject.name + ', marks:' + subject.marks }}
  </li>
</ul>
~~~

### How angular.module works?
> angular.module is used to create AngularJS modules along with its dependent modules. Consider the following example:
> 
> `var mainApp = angular.module("mainApp", []);`
> 
> Here we've declared an application mainApp module using angular.module function. We've passed an empty array to it. This array generally contains dependent modules declared earlier.

### Explain ng-include directive.
> Using AngularJS, we can embed HTML pages within a HTML page using ng-include directive.

~~~javascript
<div ng-app = "" ng-controller = "studentController">
   <div ng-include = "'main.htm'"></div>
   <div ng-include = "'subjects.htm'"></div>
</div>
~~~

### What is use of $routeProvider in AngularJS?
> `$routeProvider` is the key service which set the configuration of urls, maps them with the corresponding html page or ng-template, and attaches a controller with the same.

### What is $rootScope?
> Every application has a single root scope. All other scopes are descendant scopes of the root scope. Scopes provide separation between the model and the view. They also provide event emission/broadcast and subscription facility.

### What is a service?
> Services are JavaScript functions and are responsible to do specific tasks only. Each service is responsible for a specific task for example, $https: is used to make ajax call to get the server data. $route is used to define the routing information and so on. Inbuilt services are always prefixed with $ symbol.

### What is service method?
> Using service method, we define a service and then assign method to it. We've also injected an already available service to it.
> 
> ~~~ javascript
> mainApp.service('CalcService', function(MathService){
   this.square = function(a) { 
      return MathService.multiply(a,a); 
	}
});
~~~

### What is factory method?
> Using factory method, we first define a factory and then assign method to it.
> 
> ~~~javascript
> var mainApp = angular.module("mainApp", []);
mainApp.factory('MathService', function() {     
   var factory = {};  	
   factory.multiply = function(a, b) {
      return a * b 
   }
   return factory;
}); 
~~~

### What are the differences between service and factory methods?
> factory method is used to define a factory which can later be used to create services as and when required whereas service method is used to create a service whose purpose is to do some defined task.

### What is provider?
> provider is used by AngularJS internally to create services, factory etc. during config phase(phase during which AngularJS bootstraps itself). Provider is a special factory method with a method get() which is used to return the value/service/factory.

### Can angular applications (ng-app) be nested within each other?
> No. AngularJS applications cannot be nested within each other.

### What does SPA (Single Page Application) mean? How can we implement SPA with Angular?
> Single Page Applications (SPAs) are web apps that load a single HTML page and dynamically update that page as the user interacts with the app. In an SPA the page never reloads, though parts of the page may refresh. This reduces the round trips to the server to a minimum.

> It’s a concept where we create a single shell page or master page and load the webpages inside that master page instead of loading pages from the server by doing post backs. We can implement SPA with Angular using Angular routes. You can read up about SPAs here.


