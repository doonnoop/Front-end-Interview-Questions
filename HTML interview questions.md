## HTML interview questions
### What does a doctype do?
> DOCTYPE is an abbreviation for “document type”. It is a declaration used in HTML to tell the browser to render the web page in standards mode.
> 
> Moral of the story - just add <!DOCTYPE html> at the start of your page.

>DOCTYPE是“document type”的缩写。它是 HTML 中用来区分标准模式和怪异模式的声明，用来告知浏览器使用标准模式渲染页面。
>
>从中获得的启发：在页面开始处添加<!DOCTYPE html>即可。

### How do you serve a page with content in multiple languages?
> Use `lang=""` in tags. Also metadata and Content-Language HTTP header can be used.

### What kind of things must you be wary of when design or developing for multilingual sites?
> * href lang attr in link
> * dir attr indicating language direction, such as rtl
> * \<meta charset='UTF-8'>
> * font-size for :lang({language_code}) selectors in CSS
> * difference in word langth for each language

### What are data- attributes good for?
> Before JavaScript frameworks became popular, front end developers used data- attributes to store user's extra data within the DOM itself. But now it's not encourage, you should better store data in javascript itself.

### Describe the difference between a cookie, sessionStorage and localStorage.
> All the above-mentioned technologies are key-value storage mechanisms on the client side. They are only able to store values as strings.
> 
![aa](https://i.imgur.com/0dRtF8x.png)
> Cookie can be initial in both client and server, but localStorage and sessionStorage can only be initial in client side.
> localStorage can never expire, cookie can set expire time, and sessionStorage will expire on closeing browser.
> Cookie can be sent to server via header, while the other two cannot.
> One domain can only have 4kb cookie capacity, while the other two hav 5MB.

### Describe the difference between \<script>, \<script async> and \<script defer>.
> * \<script> - HTML parsing is blocked, the script is fetched and executed immediately, HTML parsing resumes after the script is executed.
> 
> * \<script async> - The script will be fetched in parallel to HTML parsing and executed as soon as it is available.
> 
> * \<script defer> - The script will be fetched in parallel to HTML parsing and executed when the page has finished parsing. 
> 
> Note: The async and defer attrib­utes are ignored for scripts that have no src attribute.

### Placing \<link> in the \<head>
> Putting \<link>s in the head is part of the specification. Besides that, placing at the top allows the page to **render progressively** which improves the user experience. If you put stylesheet near the bottom of the document, this may cause problems like blank white page.

### Placing \<script> just before \</body>
> \<script>s block HTML parsing while they are being downloaded and executed. Downloading the scripts at the bottom will allow the HTML to be parsed and displayed to the user first.

### What is progressive rendering?
> Progressive rendering is techniques used to improve the performance of a webpage to render content for display as quickly as possible, espicailly in modern development as mobile app.
> 
> Examples of such techniques:
> 
> * Lazy loading of images 图片懒加载 - Images on the page are not loaded all at once. JavaScript will be used to load an image when the user scrolls into the part of the page that displays the image.
> 
> * Async HTML fragments 异步加载 HTML 片段 - Flushing parts of the HTML to the browser as the page is constructed on the back end.
> 
> 渐进式渲染是用于提高网页性能，以尽快呈现页面的技术，现在在移动端流行。

### Why you would use a srcset attribute in an image tag?
> You would use the srcset attribute when you want to serve different images to users depending on their device display width.
> 
> For example: \<img srcset="small.jpg 500w, medium.jpg 1000w, large.jpg 2000w" src="..." alt=""> tells the browser to display the small, medium or large .jpg graphic depending on the client's resolution. 
> 
> For a device width of 320px, the following calculations are made:
> 
> * 500 / 320 = 1.5625
> * 1000 / 320 = 3.125
> * 2000 / 320 = 6.25
> 
> If the client's resolution is 1x, 1.5625 is the closest, and 500w corresponding to small.jpg will be selected by the browser.
> 
> If the resolution is retina (2x), the browser will use the closest resolution above the minimum. Meaning it will not choose the 500w (1.5625), the browser would then choose the image with a resulting ratio closer to 2 which is 1000w (3.125).

### Have you used different HTML templating languages before?
> Pug (formerly Jade), Nunjunks, JSX. In my opinion, they are provide similar functionality of displaying content and helpful filters for manipulating the data to be displayed. 

## HTML 5
### New HTML5 Elements
> * New **semantic elements** like \<header>, \<footer>, \<article>, and \<section>.
> * New attributes of form input elements like number, date, time, calendar, and range.
> * New graphic elements: \<svg> (javascript) and \<canvas> (vector).
> * New multimedia elements: \<audio> and \<video>.

### New HTML5 API's
> The HTML Geolocation API is used to locate a user's position.
> 
> Drag and drop is a very common feature. It is when you "grab" an object and drag it to a different location. In HTML5, drag and drop is part of the standard: Any element can be draggable.
> 
> HTML5 web storage; better than cookies. With web storage, web applications can store data locally within the user's browser.

### Removed Elements in HTML5
> remove \<center>, \<font> and use in CSS instead.
