# CSS Notes

CSS is all about **property: value;** pairs.

Inline CSS is usually implemented through JS. It is otherwise bad practice.

`<link href="index.css" rel="stylesheet">` specifies the reference CSS file and its relationship to the HTML document.

CSS code is executed from the top up so lower lines will overwrite the first ones.

## The Box Model

* **Margin** is the empty space outside an element. It will create space between the entire box and the elements surrounding it. `margin: 10px;` will give the value to all four sides, and it is equivalent to `margin: 10px 10px 10px 10px;`. The order in the shorthand is clockwise from the top. Top-Right-Bottom-Left.
* **Padding** is the empty space inside an element, so it will include a background in the box. Same syntax as above.
* **Borders** are situated around the box and take width, style and color values. Borders can be controlled individually, such as `border-bottom: blue`.

Need empty space: margin.
Need more background: padding.

Margin is setup by default as the same number of the font size in a container. So, 16px font size means a 16px default margin.

`Margin-bottom` and `margin-top` on block elements will not add up to each other. If one is 20px and the other is 50px, the biggest one will be, so the value will be 50px.

Margins between parent and child can collapse, meaning a margin on the child element will be automatically applied to the parent. For example, margin-top on a text element within a div container. The solution to this is to add `padding` to the parent, then the margin on the child will not collapse.

Margins do not collapse on flexbox and grid.

```css
div.card {
    background: #000;
    color: white;
    width: 560px;
    margin: 0 auto;
    padding: 50px;
}
h1.links {
    font-size: 24px;
    margin-top: 45px;
}
```

For consistency, it's better to set a `margin-top` of 0 to multiple elements and `margin-bottom` 0 to the last element.

```css
h1, h2, h3, p {
    margin-top: 0px;
}
p.links {
    margin-bottom: 0px;
}
```

Inline element only accept left and right margin, not top and bottom.

`Margin-left: auto` will push everything to the right, and viceversa.

## Box Sizing Change

The default height and width of a container are set on `content-box`. This means that they are calculated on the width value, plus padding, border and margin. The code below will change all box-sizing on the page to `border-box`. This will instead calculate the height and width based on those two values alone.

```css
* {
    box-sizing: border-box;
}
```

## Evenly-Padded Containers

Padding is included inside the total container width. So, if a container is meant to be 500px, do the following to ensure even padding on all sizes. The margin property will make it responsive to the screen size.

```css
.blog-post {
    background: #f1f1f1;
    width: 450px;
    padding: 25px;
    margin: 0 auto;
}
```

## Display inline-block

Inline elements cannot have margin or padding on the top and bottom. When this is required, the elements can be changed to `inline-block`. This is usually done for buttons. Buttons should be given a size with padding, never with width and height. If doing this on a link, set up the class on the link, not the paragraph.

The code below will style a link properly and turn it into a button without using the `<button>` tag, though everything can be applied to a `<button>` tag as well. The padding ratio is 1:2 to 1:3 for top/bottom:left/right.

```css
.button {
    display: inline-block;
    background: #FFE600;
    color: black;
    padding: 15px 30px;
    text-align: center;
    text-decoration: none;
    margin-bottom: 50px;
}
.button:hover {
    background: orange;
}
```

## CSS selectors

For styling purposes, use classes or elements.

* Elements `div`.
* Classes `.class-name`. Used over and over on a page.
* ID `#id-name`. Used once per page, will overwrite a class selector.

`<span>` can be used to style an independent element, but they should be used with a class selector.

## Centering Content and Containers

* `text-align: center;` will align the text to the center within the viewport, but only the the text or contents, not the container itself.
* In order to center a container on page, it must have a width and `margin-left` and `margin-right` must be set to auto, or `margin: 0 auto`, where 0 is top and bottom, auto is left and right.

## Styling Semantic Tags

Styling should be done on text tags, not semantic tags. This is because the semantic tags will scale the overall size. `<p>` with a size of 72px will actually be 72px, meanwhile `<header>` with a `font-size: 72px` on everything will make a `<h1>` tag bigger than a `<p>` within itself.

## Gradient Background

A gradient background can be rendered with CSS without images.

```css
background-image: linear-gradient(#5DA4D9, lightgrey);
```

## Decorating Links

Style them in the same order as this list.

* `a:link` and `a:visited` are the regular link and the visited ones.
* `a:focus` is a link selected with the tab key.
* `a:hover` is the one you're over.
* `a:active` is the moment you are clicking on a link.

## Selectors Specificity

Selectors have a priority order. IDs > Classes > Element.

Classes are used for styling things. IDs are useful for unique elements that need to be hooked up with JS.

The below code will make the text green **only** to the div elements inside the .grid class.

```css
.grid div {
    color: green;
}
```

## Compound selectors

They can be used when certain elements are identical to each other except for a few style differences. Use them only if necessary. The example below could have been easily replaced by two different classes such as btn-yellow and btn-black.

```css
.section-one .btn {
    display: inline-block;
    padding: 12px 25px;
    background: #FFE600;
    color: #000;
    font-weight: bold;
    text-decoration: none;
}

.section-two .btn {
    display: inline-block;
    padding: 12px 25px;
    background: #FFE600;
    color: #000;
    font-weight: bold;
    text-decoration: none;
}
```

The best practice is to use multiple classes.

```html
<a href="#" class="btn btn-accent">learn more about me</a>
```

```css
.btn {
    display: inline-block;
    padding: 12px 25px;
    font-weight: bold;
    text-decoration: none;
}

.btn-accent {
    background: #FFE600;
    color: #000;
}

.btn-dark {
    background: #000;
    color: #fff;
}
```

## Typography

Fonts can slow a page down greatly, so only load a few at a time. You can import them through Google Fonts.

For other text properties, [see pdf cheatsheet here](/Other/css-font-properties.pdf).

The below will make a `span` element with `.bolt-text` class appear bold, and on a new line by changing the default `display: inline`. Much better than using `<br>`.

```css
.bold-text {
    font-weight: 900;
    display: block;
}
```

Font-sizes automatically setup the default margins in CSS. Add margin-bottom to text element, especially to large titles. A lot of margin issues come from text.

## Position

Elements can be positioned in different parts of a page using `position`. The value `relative` will turn a parent element into an anchor point for another element with value `absolute`. The below absolute child will overlay the parent on the top and right margin. These values can be changed to move containers around the page. Absolute elements will always anchor to the nearest parent. Elements with `position: fixed` will instead position themselves according to the viewport and ignore the flow of the page.

```css
#parent2 {
  position: relative;
  border: 1px solid blue;
  width: 300px;
  height: 100px;
}

#child2 {
  position: absolute;
  border: 1px solid red;
  top: 0px;
  right: 0px;
}
```

## Pseudoclasses

Adding `:last-child` to a parent element will target its last child.

```css
.widget-recent-post:last-child {
    border: 0;
    margin: 0;
}
```

## Pseudoelements

Pseudo elements are used to add decorative elements and have two semicolons. They add an html element inside the element you are targetting. They should have `content: ""` so they don't overwrite anything, and either `display` or `position` to make them stay in place.

`h1::before` would load inside an `<h1>` tag, but before the content.
`h1::after` is still inside, but after the content.

The example below creates a centered decorative underline.

```css
.section-title::after {
    content: "";
    display: block;
    width: 60px;
    height: 3px;
    margin-top: 10px;
    background: #FFE600;
    margin-left: auto;
    margin-right: auto;
}
```

## More Selectors

Combinators:

* `h1 + p {}` will select only one `<p>` element that come after an `<h1>` element.

* `h1 ~ p {}` will select all the sibling `<p>` elements that come after an `<h1>` element.

* `.intro > p {}` will select any `<p>` elements that are direct children of class intro.

Others:

* `.intro * {}` will select everything inside the class intro.

* `input[type="text"]` will only select form inputs with text type. These are called attribute selectors. Classes are a better choice for styling forms though.

## CSS Variables

Declare a global variable in the root pseudo element, which references the `html` tag.

```css
:root {
    --red: #ff6f69;
}
```

That variable can then be referenced anywhere in the stylesheet.

```css
body {
    color: var(--red);
}
```

Variables can also be declared and overwritten anywhere else in a parent, but only its children will be able to reference it. This can be used to create different styles for certain parts of a website, such as a featured item, or a sold out product in an e-commerce site.

Styles can also be accessed through the DOM.

```js
let root = document.querySelector(':root');
let rootStyles = getComputedStyle(root);
let yellow = rootStyles.getPropertyValue('--yellow');
root.style.setProperty('--yellow', 'orange');
```
