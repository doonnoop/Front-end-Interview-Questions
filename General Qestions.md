## General Qestions
### What UI, Security, Performance, SEO, Maintainability or Technology considerations do you make while building a web application or site?
> * **UI**: I like minimal UI which contains only what it should. I believe it results in the better user experience, as a user knows what to do intuitively.
> * **Security**: I always try to make both frontend and backend secure, like crypt for the password or not include database information in the code.
> * **Performance*: I consider space and time complexity for the algorithms and logics I use and write.
> * **SEO**: Set meta tags for search engines and consider and consider server-side rendering for SPA.
> * **Maintainability**: Try to keep the source code consistent and make objects immutable. Use statically typed languages such as TypeScript. Use CI with tests and lints.
> * **Technology**: I like to learn new technologies, but if the project is in production, I would consider using technologies which is well-documented and widely used.

### Talk about your preferred development environment.
> Linux, OS X, iterm, webstorm, Atom

### Which version control systems are you familiar with? 
> Git

### Can you describe your workflow when you create a web page?
> I usually use Node.js to build a web page, so will describe the workflow with it.
> 
> * Decide a CSS preprocessor. 
> * Decide a HTML template engine. 
> * Decide a JavaScript preprocessor or other languages being compiled to it. I may go with TypeScript or ES6 with Babel.
> * Decide a task manager. I recently like to just use NPM scripts instead of using huge task managers like Gulp or Grunt.
> * Write tests and make them fail.
> * Write app code and check the tests succeed.

### If you have 5 different stylesheets, how would you best integrate them into the site?
> Use a CSS preprocessor to nest them with @import statements in class names for each stylesheet, and merge them into a built file. In production, minify the built file with a CSS minifier.

### Describe how you would create a simple slideshow page.
~~~CSS
<div class='slide-page'>...</div>
<div class='slide-page'>...</div>
<div class='slide-page'>...</div>
~~~

~~~css
html, body, .slide-page {
  width: 100%;
  height: 100%;
}

.slide-page {
  position: fixed;
  top: 0;
  left: 0;
  display: none;
}

.slide-page:first-child {
  display: block;
}
~~~

~~~javascript
window.addEventListener('click', () => {
  document.querySelector('.slide-page').remove();
});
~~~

### What are some advantages/disadvantages to testing your code?
> **Advantages**: Prevent regression errors; Ensure there is no missing part to change when refactoring; Tests can be used as specs; Test process can be shared amongst team members
> 
> **Disadvantages**: It may or may not take more time to prototype.

### What tools would you use to test your code's functionality?
> For JavaScript, the basic `assert` module is quite enough for simple tests. But when it gets a big and production-level project, it is a better idea to set a test framework. For backend, I usually use Mocha. For frontend, Mocha can still be used with headless browsers such as PhantomJS. Th