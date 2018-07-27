## CSS interview Questions
### What is CSS selector specificity and how does it work?
> The browser determines what styles to show on an element depending on the specificity of CSS rules. Among the matching rules, four comma-separate values, a, b, c, d are calculated for each rule based on the following:
> 
> 1. **a** is whether inline styles are being used. If the property declaration is an inline style on the element, a is 1, else 0.
> 2. **b** is the number of ID selectors.
> 3. **c** is the number of classes, attributes and pseudo-classes selectors.
> 4. **d** is the number of tags and pseudo-elements selectors.
> 
> When comparing selectors to determine which has the highest specificity, look from left to right, and compare the highest value in each column. In the cases of equal specificity: the latest rule is the one that counts. 当出现优先级相等的情况时，最晚出现的样式规则会被采纳。
> 
> I would write CSS rules with low specificity so that they can be easily overridden if necessary, so that users of the library can override them without using too complicated CSS rules just for the sake of increasing specificity or resorting to **!important**. 这样使用者就不需要通过非常复杂的优先级规则或使用!important的方式，去覆盖组件的样式了。

### What's the difference between "resetting" and "normalizing" CSS? Which would you choose, and why?
> * **Resetting** - Resetting is meant to strip all default browser styling on elements. For e.g. margins, paddings, font-sizes of all elements are reset to be the same. You will have to redeclare styling for common typographic elements.
> * **Normalizing** - Normalizing preserves useful default styles rather than "unstyling" everything. It also corrects bugs for common browser dependencies.
> 
> I would choose resetting when I have a very customized or unconventional site design such that I need to do a lot of my own styling and do not need any default styling to be preserved.

### Describe **floats** and how they work.
> Float is a CSS positioning property. When float is set, each element will get out of its normal flow and will be shifted to the specified direction. Floated elements remain a part of the flow of the page, and will affect the positioning of other elements (e.g. text will flow around floated elements), unlike position: absolute elements, which are removed from the flow of the page.
> 
> 浮动（float）是 CSS 定位属性。浮动元素从网页的正常流动中移出，但是保持了部分的流动性，会影响其他元素的定位（比如文字会围绕着浮动元素）。这一点与绝对定位不同，绝对定位的元素完全从文档流中脱离。

### Describe z-index and how stacking context (层叠上下文) is formed.
> The z-index property in CSS controls the vertical stacking order of elements that overlap. z-index only affects elements that have a position value which is not static.
> 
> Without any z-index value, elements stack in the order that they appear in the DOM (the lowest one down at the same hierarchy level appears on top 层级越低，出现位置越靠上). Elements with non-static positioning will always appear on top of elements with default static positioning, regardless of HTML hierarchy.

### Describe Block Formatting Context (块格式化上下文) and how it works.
> BFC is part of the visual CSS rendering of a web page in which block boxes are laid out. It establish new block formatting contexts with float and other elements (inline-block etc.) when: 
> 
> * The value of `float` is **not** `none`.
> * The value of `position` is **neither** `static` nor `relative`.
> * The value of `display` is `table-cell`, `table-caption`, `inline-block`, `flex`, or `inline-flex`.
> * The value of `overflow` is **not** `visible`.

### What are the various clearing float techniques and which is appropriate for what context?
> * Empty `div` method: `<div style="clear:both;"></div>`.
> * Clearfix method:
>  
 ~~~css
 .clearfix:after {
 		content: ' ';
 		visibility: hidden;
 		display: block;
 		height: 0;
  		clear: both;
 	}
 ~~~
> * `overflow: auto` or `overflow: hidden` method: Parent will establish a new block formatting context and expand to contains its floated children.

### Explain CSS sprites (雪碧图), and how you would implement them on a page or site.
> CSS sprites combine multiple images into one single larger image. It is a commonly-used technique for icons (Gmail uses it). How to implement it:
> 
> 1. Use a sprite generator that packs multiple images into one and generate the appropriate CSS for it.
> 2. Each image would have a corresponding CSS class with `background: url(...) x-axis y-axis;` or `background-image`, `background-position` and `background-size` properties defined.
> 3. To use that image, add the corresponding class to your element.
> 
> **Advantages:**
> 
> * Reduce the number of HTTP requests for multiple images
> * Loading asset ahead, avoid the problems that happen downloaded until needed.

### How would you approach fixing browser-specific styling issues?
> * Use libraries like Bootstrap that already handles these styling issues for you.
> * Use autoprefixer to automatically add vendor prefixes to your code.
> * Use Reset CSS or Normalize.css.
> * After identifying the issue and the offending browser, use a separate style sheet that only loads when that specific browser is being used. This technique requires server-side rendering though.

### What are the different ways to visually hide content?
> * `visibility: hidden`. However, the element is still in the flow of the page, and still takes up space.
> * `width: 0; height: 0`. Make the element not take up any space on the screen at all, resulting in not showing it.
> * `position: absolute; left: -99999px`. Position it outside of the screen.
> * `text-indent: -9999px`. This only works on text within the block elements.
> * Metadata. For example by using Schema.org, RDF, and JSON-LD.
> 
> I would go with the absolute positioning approach, as it has the least caveats, works for most elements and it's an easy technique.

### Have you ever used a grid system, and if so, what do you prefer?
> I like the `float`-based grid system because it still has the most browser support. It has been used in Bootstrap for years.

### Have you used or implemented media queries or mobile-specific layouts/CSS?
> Yes. An example would be transforming a stacked pill navigation format as the window size changed. (Bootstrap: @media sm-12, md-8)

### CSS preprocessors
> To handle the problems caused by origin CSS, like SASS, LESS (combine with javascript and NodeJs), which is easy to use and maintain.

### How would you implement a web design comp that uses non-standard fonts?
> Use `@font-face` and define `font-family` for different `font-weight`s.

### Explain how a browser determines what elements match a CSS selector.
> Browsers match selectors from rightmost (key selector) to left. 
> 
> * Browsers first check matching elements for the key(right-most) selector,
> * and then check if the elements are matching parents for the next selectors. 
> 
> The shorter the length of the selector chain, the faster the browser can determine if that element matches the selector.
> 
> For example with this selector `p span`, browsers firstly find all the `<span>` elements and traverse up its parent all the way up to the root to find the `<p>` element. For a particular `<span>`, as soon as it finds a `<p>`, it knows that the `<span>` matches and can stop its matching.

### Describe pseudo-elements and discuss what they are used for.
> A CSS pseudo-element is a keyword added to a selector that lets you style a specific part of the selected element(s).
> 
> * `:first-line` and `:first-letter` can be used to decorate text.
> * Used in the `.clearfix` hack as shown above to add a zero-space element with `clear: both`.
> * Triangular arrows in tooltips use `:before` and `:after`.

### Explain your understanding of the box model.
> ![](https://i.imgur.com/nGOp3D3.png)
> The CSS box model describes the rectangular boxes that are generated for elements in the document tree and laid out according to the visual formatting model. It consists of: margins, borders, padding, and the actual content. 

### What does `* { box-sizing: border-box; }` do? What are its advantages?
> * By default, elements have `box-sizing: content-box` applied, and only the content size is being accounted for.
> * `box-sizing: border-box` changes how the width and height of elements are being calculated, border and padding are also being calculation.
> * The `height` of an element = the content's `height` + vertical `padding` + vertical `border` width.
> * The `width` of an element = the content's `width` + horizontal `padding` + horizontal `border` width.
> 
> Taking into account paddings and borders as part of our box model explain how designers actually imagine content in grids.

### What is the CSS `display` property and can you give a few examples of its use?
> `none`, `block`, `inline`, `inline-block`, `table`, `table-row`, `table-cell`, `list-item`.
> 
> [display demo, click to see how it use](https://www.w3schools.com/cssref/playit.asp?filename=playcss_display&preval=inline)
> 
> * `inline`: Displays an element as an inline element (like \<span>). Any height and width properties will have no effect.
> * `block`: Displays an element as a block element (like \<p>). It starts on a new line, and takes up the whole width.
> * `inline-block`: Displays an element as an inline-level block container. The element itself is formatted as an inline element, but you can apply height and width values.
> * `table-row`: Let the element behave like a \<tr> element.
> * `table-cell`: Let the element behave like a \<td> element.
> * `list-item`: Let the element behave like a \<li> element.

### What's the difference between `inline` and `inline-block`?
> ![e](https://i.imgur.com/b4KA129.png)

### What's the difference between a `relative`, `fixed`, `absolute` and `static` element?
> * `static` - The default position; the element will flow into the page as it normally would. The `top`, `right`, `bottom`, `left` and `z-index` properties do not apply.
> * `relative` - The element's position is adjusted relative to itself, without changing layout (leaving a gap for the element where it would have been had it not been positioned).
> * `absolute` - The element is removed from the flow of the page and positioned at a specified position relative to its closest positioned ancestor. Absolutely positioned boxes can have margins, and they do not collapse with any other margins. These elements do not affect the position of other elements.
> * `fixed` - The element is removed from the flow of the page and positioned at a specified position relative to the viewport and doesn't move when scrolled.
> * `sticky` - Sticky positioning is a hybrid of relative and fixed positioning. The element is treated as relative positioned until it crosses a specified threshold, at which point it is treated as fixed positioned.

### What existing CSS frameworks have you used locally, or in production?
> * Bootstrap is widely used and now is alpha version 4
> * Materialized-CSS is a flattening format.

### How is responsive design different from adaptive design?
> Both responsive（响应式） and adaptive design（自适应） attempt to optimize the user experience across different devices, adjusting for different viewport sizes, resolutions, usage contexts, control mechanisms, and so on.
> 
> Responsive design works on the principle of flexibility: There is one basic layout, and it changes responsively to screen changes.
> 
> Adaptive: For each possible screen size, there is a distinct layout. 

### What are your favourite image replacement techniques and which do you use when?
> Image replacement technique is to replace a normal text element with an image. I know one is H5BP, as it is the simplest.

### What are some of the "gotchas" for writing efficient CSS?
> * Avoid key selector for large numbers of elements
> * Prefer class and ID selector to tag selector
> * Avoid redundant selectors
> * Care of batching

### The 'C' in CSS stands for Cascading. How is priority determined in assigning styles (a few examples)? How can you use this system to your advantage?
> CSS priority is determined by specificity and inheritance.
> 
> * Specificity: ID > class, psuedo-class > element, psudo-element
> * Inheritence: specified value → computed value → used value → actual value

### What are the differences between visibility hidden and display none?
> `display: none` removes the element from the normal layout flow and allow other elements to fill in. causes DOM reflow 
> 
> `visibility: hidden` tag is rendered, it takes space in the normal flow but doesn't show it.

### Does `overflow: hidden` create a new block formatting context?
> Yes. Overflow property deals with the content if content size exceeds the allocated size for the content. You can make extra content visible, hidden, scroll or auto.

### How do you align a p center-center inside a div?
> `text-align: center` will do the horizontal alignment but `vertical-align: middle` will not work here.
> 
> You make the parent as relative position and child as absolute positioning. And then define all position parameter as 0 and width 50% and height 30%.
> 
~~~css
<style>
   .divContainer{
      height: 100px;
      border: 2px solid gray;
      text-align: center;
      position: relative;
   }
   p{        
      position: absolute;
      top: 0;
      bottom: 0;
      left: 0;
      right: 0;
      width: 50%;
      height: 30%;
      margin: auto;
    }
</style>
~~~