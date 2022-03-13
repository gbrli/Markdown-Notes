# Responsive Design

## Units

There are three types of units in CSS.

* Absolute units are a fixed value
* Percentages are relative to their parent, but it's good practice to only use them for width, never height.
* Relative units can be relative to the font-size such as `em` and `rem` or to the viewport such as `vh`, `vw`, `vmin` and `vmax`.

Percentage values are ideal for container divs. The percentage refers to the parent, and in most cases the parent elements are set to 100% width.

Images within a container should have width 90% because they are relative to their parent. If the parent container is set with width 70%, that is relative to a higher parent. So the image will be 90% of that reserved 70%.

## Font Units

Em works with percentages. `font-size: 1.5em` means 150% of the font-size of the parent element. This can be a problem with nested elements: `<li>` font size will be relative to `<ul>` font size, and up until the body.

`Rem` stands for root em. This unit resolves the nesting issue above because rem units are relative to the root, meaning the `<html>` element. The html element has a default font size set to 16px. The tag below will set it to 10px. All fonts in the document should then use rem as a unit instead of px.

```css
html {
    font-size: 62.5%;
}
```

## Converting px to rem (font size)

1rem = 16px. So, if you have an element with 42px size, divide it by 16 and you get 2.625rem.

`42 / 16 = 2.625`

## Converting px to em (padding/margin)

Em units are relative to the font size in the current element, so if you have 20px padding and a font size of 2.625rem, do the below.

`2.625 * 16 = 42 - back to the pixel unit`

`20 / 42 = 0.48em - 20px become 5em rounded up`

**If no font size is specified on an element, the default should always be 16px!**

## Viewport Units

These units are relative to the viewport size. The below will set the height and width of the header section to the total height and width of the viewport.

```css
header {
    height: 100vh;
    width: 100vw;
}    
```

`vmin` and `vmax` will do the same, but they will match the size with the smallest or biggest value between height and width. Their usage is less common.

## Flexbox

Block elements in html are set by default as `display: block`, and will stack on top of each other, creating a long list of rows. Setting `display: flex` on a container, will turn all those rows into columns instead.

The initial markup is the most important part in setting up flexbox. The entire flex layout should be in a container to be safe. Then, there should be a container for all the columns in each row, and one for each individual column inside it.

**Each column should be in a div!**

`Width` and `max-width` are different units, and they do not override each other. A flex element can have both properties. One simple solution is having widths that add up to 90% or so, and than the property below. The remaining 10% will be the space between elements. `Justify-content` will space things on the horizontal axis.

`justify-content: space-between;`

 Spacing on the vertical axis is done with `align-items`. When `display: flex` is applied, the block elements in rows turn to columns and stretch to 100% of the vertical axis. Changing the alignment of the items to `flex-start` or `center` will change the default `stretch`.

## Changing the vertical axis

If `flex-direction` is set to `columns` instead of the default `row`, the vertical axis will be inverted and the layout will go back to looking like the initial block elements, but with all the benefits of flex. **However, `justify-content` and `align-items` will work on the opposite axis instead.**

## Changing the item order in flexbox

The logical order of the markup elements should be maintained. If a stylesheet is not loaded, the website should still be readable. Flexbox allows to change the orders of markup elements with `order: 2` on the child elements, provided the parent contains the `display: flex property.`

## Negative Margins

They are not the best practice, but they can be used if necessary. `margin-top: -5em` will position an element up by 5em. Be careful about overlap. Try using `margin-bottom` on the element above first.

## Working mobile first

Layouts should be created for mobile first. This is because desktop websites require more code and more detail compare to a mobile version. Media queries to adjust a design to mobile will have to overwrite more of the original code, meanwhile doing the opposite means you're only adding the code for the desktop page.

## Media Queries

They are properties in CSS that allow to add styles if certain conditions are met. They work like an if statement. If the condition in the media query is met, the code below is executed. The example below changes the background to purple when the width goes over 400px. Note the nesting.

```css
body {
    background: pink;
}
@media (min-width: 400px) {
    body {
        background: purple;
    }
}
```

Media queries are executed in order with the rest of the code, so they should be placed after the default value have been established.

## Styling

Font weights should be declared with a number because browsers will interpret them differently. For example, Firefox sets `bold` to 900 instead of the standard 700, meaning `bold` and `bolder are the same.

Also, if you have imported a font with Google and it comes in different sizes (300, 400, 700), `<strong>` will select the next available size by 100. So, if you have a paragraph with `font-weight: 300` and you make something bold in there, it will only be 400, not 700.

Images can appear cropped with the `object-fit` property. The `min-height` property would normally stretch the image, but with `object fit: cover` it will zoom in on the center. The zooming can be also position with `object-position`.

```css
    .article-image {
        width: 100%;
        min-height: 500px;
        object-fit: cover;
        object-position: left;
    }
```

## Breakpoints for Media Queries

Breakpoints should be added when the layout stops working. Not according to any device size.

## Styling Tips

* Avoid fixed set widths, use a percentage, or em.
* Font sizes in rem, margin/padding in em
* Rem is relative to the root html tag. Em is relative to the font size in each element. Changing the root value will scale everything to proportion. `html > rem > em`
* Give space to all four sides of the main page container with `width: 90%`. Alternatively, use padding, but the first solution is cleaner.
* Don't be afraid to add a `<div class="flex>` with the only purpose of making something two columns. It won't mess up the rest of the layout.
* If an element has two classes, use selectors for both, even if you only need one. This will improve the specificity of the selector and it's safer in the long run.
* `color: currentColor` will inherit the property from the parent element.
* **Don't use padding to justify elements within a container. Use flexbox instead.**

## Typography

* `line-height` is equally distributed up and down. Ideally leave it between 1.4 and 1.7, because at 2 it becomes double spaced and harder to read. Big text and uppercase text require a smaller line-height.
* `text-transform` is usually used with uppercase, lowercase or capitalize. It is useful because rewriting may cause typos.
* `letter-spacing` will leave space between individual letters. Keep it on the lower end of 1 to 2 unless it's required by a design.
* Longer lines of text are annoying to read on large screens, so put a max-width that works with the layout on the `<p>` element using a class.

## Positioning

`Position: absolute` removes a container from the natural flow of the page, isolating it.

Make something stuck to the top left:

```css
img {
    position: fixed;
    top: 0;
    left: 0;    
}
```

Use the same property to create a nav bar that remains fixed in the middle of the screen on mobile.

```css
.nav {
    position: fixed;
    background: #000;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
}
```

To open and close the navbar, the translateX property is used with the left positioning.

```css
.navigation-open {
    left: 100%;
    transform: translateX(0);
}

.navigation-open {
    transform: translateX(-100%);
}
```

`position: initial` will bring an element back to where it was. Useful in a media query to revert to the original state.

A background can be transparent and overlapping over an image.

```css
.header-home {
    background: transparent;
    position: absolute;
    width: 100%;
}
```
