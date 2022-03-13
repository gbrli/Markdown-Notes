# Templates

## Basic HTML Doc

Basic setup for any doc:

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Title</title>
        <link rel="preconnect" href="https://fonts.gstatic.com">
        <link href="https://fonts.googleapis.com/css2?family=PT+Sans:ital,wght@0,400;0,700;1,400&family=Source+Sans+Pro:wght@900&display=swap" rel="stylesheet">
        <link href="index.css" rel="stylesheet">
    </head>
    <body>
      <header></header>
      <section></section>
    </body>
</html>
```

## CSS Starting Point

```css
body {
    margin: 0;
    font-size: 1.125rem;
    color: black;
}

h1, h2, p {
    margin-top: 0;
}

h1 {
    font-size: 24px;
}

p {
    font-size: 18px;
}

a {
    color: #FFE600;
}

img {
  max-width: 100%;
  display: block;
}
```

## CSS Starting Point 2.0

```css
*,
*::before,
*::after {
    box-sizing: border-box;
}


body {
    margin: 0;
    font-family: 'Montserrat', sans-serif;
    font-size: 1rem;
    color: #404040;
    line-height: 1.6;
}

h1, h2, strong {
    font-weight: 700;
}
```

## Flexbox Structure

It's okay to have container for the sake of containing and styling. The three flex columns are inside a columns div, and all inside the container. `display: flex` on the parent `columns` can be nested within another `<div class="columns">` to achieve a double column layout.

```html
  <section class="accent-bg">
    <div class="container">
      <div class="columns">
        
        <!-- column 1 -->
        <div class="col">
        </div>
          
        <!-- column 2 -->
        <div class="col">
        </div>
        
        <!-- column 3 -->
        <div class="col">
        </div>
      
      </div>
    </div> <!-- close container -->
  </section>
```

## Hamburger Menu Icon and Close Button

```html
<button aria-label="Menu" class="open-nav">&#9776;
</button>

<button aria-label="Close navigation" class="close-nav">&times;</button>
```

## Background Image Hero Section

Most used front page style with a large image as a background and text on top.

```css
.hero { 
    text-align: left;
    padding: 14rem 0 25rem;
    background-image: url("img/moon.jpg");
    background-size: cover;
}
```

## Responsive Input Field

Input field with side padding. The width does not include the padding so it stretches over 100% of the viewport. With box-sizing, it now moves with the page width.

```css
input {
    width: 100%;
    padding-left: 10px;
    padding-right: 10px;
    box-sizing: border-box;
}
```

## Centering an Image

Images are by default inline elements. The below will center them on a page:

```css
.center {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
```

## Flexbox Navbar

Lists come with a default padding even if you remove the bullet points, hence the `padding: 0;`.

```css
nav ul {
    list-style: none;
    padding: 0;
    display: flex;
    justify-content: center;
}
nav li {
    margin: 0 1em;
}
```

## Header as full page

The below will make the header section full page and center everything vertically.

```css
header {
    min-height: 100vh;
    display: flex;
    align-items: center;
}
```

## Background Image

Most useful setup for background images. Always place a background color similar to the image in case the latter doesn't load. It won't break the readability of the design.

```css
body {
    background-color: #404040;
    background-image: url();
    background-position: center;
    background-size: cover;
}
```

## Gradient Backgrounds Examples

```css
.box-1 { background-image: linear-gradient(to bottom right, red, blue); }

.box-2 { background-image: linear-gradient(0deg, green, yellow)}

/* .box-3 { background-image: linear-gradient(90deg, orange 75%, teal) } */

.box-4 { background-image: linear-gradient(90deg, orange 75%, teal 75%) }

.box-5 { background-image: radial-gradient(red, blue);
          width: 300px;
          height: 300px; }
```

## Simple Transitions

This property allows for an animated hover effect. Keep the value between 250ms and 500ms or it's too slow. The property needs to be on the actual element, not on the :hover.

```css
.btn {
    transition: 250ms;
}
.btn:hover, 
.btn:focus {    
    color: red;
}
```

## Scale

Scale will make an element become bigger or smaller. Note that transitions can be placed on any element, even input fields in a form.

```css
.btn {
    transform: scale(1);
    transition: transform 250ms;
}
.btn:hover,
.btn:focus {
    transform: scale(1.1);
}
```

## Gradient on Border Image

```css
.text {
    border-top: 5px solid #F18119;
    border-image: linear-gradient(to left, #ff713b, #ffa51d) 1;
}
```

## Blending Images

`Background-blend-mode` works like blending in Photoshop. The image needs to have both an image (or a gradient) and a background color. Multiply, screen and overlay are the most useful properties.

```css
container {    
    background-image: url(images/ribs.jpg), linear-gradient(45deg,red, blue);
    /* background-color: #ff0000; */
    background-blend-mode: multiply;
    background-size: cover;
    background-position: center;
}    
```

## Centering with Grid

```css
html, body {
    margin: 0;
    padding: 0;
    height: 100vh;
}

body {
    font-family: 'Montserrat';
    display: grid;
    place-content: center;
}
```

## Centering with Flex

The body of a page starts off with 0 height/width and grows with the content. A background color will take up the whole page, but a border will show the real size of the body. The code below will use flex to center in the middle.

```css
body {
  margin: 0;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
```

## Basic Grid Layout

```css
.grid {
  display: grid;
  grid-template-columns: 150px 150px 200px;
  grid-template-areas: 
    "sidebar header header" 
    "sidebar content content"
    "sidebar footer footer";
}

.header {
  grid-area: header;
}

.sidebar {
  grid-area: sidebar;
}

.big {
  grid-area: content;
}

.footer {
  grid-area: footer;
}

.grid-item {
  background: #B823C1;
  color: white;
  padding: 1em 2em;
  border: 2px solid purple;
  display: flex;
  align-items: center;
  justify-content: center;
}

.big {
    padding: 3em 2em;
    background: #FF5670;
}
```

## Responsive Grid Layout

```css
.portfolio {
    padding: 1em;
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    grid-gap: 1em;
}
```

## Responsive Body Background Image

```css
body {
    background: no-repeat center center fixed; 
    -webkit-background-size: cover;
    -moz-background-size: cover;
    -o-background-size: cover;
    background-size: cover;
}
```

## 12-Column Grid

The below repeats 12 columns that each take 1/12th of the available space. Have children span x columns.

```css
.a-pokemon {
    display: grid;
    grid-template-columns: repeat(12, calc(100% / 12));
}
```
