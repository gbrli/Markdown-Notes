# UI Design

There are 7 fundamental elements to good UI design:

* White space
* Alignment
* Contrast
* Scale
* Color
* Typography
* Visual Hierarchy

A good design will give importance to all seven of them.

Avoid absolute black for backgrounds, especially if there's white text, as it can cause eye strain. Use something like #1c1c1c instead.

## Decorations with ::before (pseudoelement)

The property ::before can be used to decorate container with `z-index`, or more. The example below creates a blue stripe on the background on the left.

```css
.container:before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 20%;
    background: #E4F0FF;
    height: 100vh;
    z-index: -1;
}
```

Another one that gives an offset underline.

```css
span {
    position: relative;
}

span:before {
    position: absolute;
    content: '';
    height: .2em;
    width: 80%;
    bottom: .1em;
    z-index: -1;
    background: #e88a62; 
}
```

## Drop Shadows

Use them carefully or they look dated. They look best when they are subtle, not too thick, and with low contrast. You can use color but they should never stand out more than the actual page content.

Ideal soft shadow:

`box-shadow: 10px 10px 10px rgba(0,0,0,0.1);`

Ideal hard shadow:

`box-shadow: 0px 4px 3px rgba(0,0,0,0.1);`

You can also use shadows to define containers instead of using a border. Make it show more sides like the hard shadow, or use a soft one like this:

`box-shadow: 10px 10px 30px rgba(0,0,0,0.15);`

Colored shadows are best used on a light background, with a hue that doesn't contrast any other elements, or one that blends into the background.

This shadow below is solid, and contains two layers, one black, one yellow.

```css
box-shadow: 
    5px 5px 0px black, 
    10px 10px 0 #FFE600;
```


## Use image as hero background
Using z-index at -1 will make the image become the background for the next section in the markup. Position absolute is required.

```css
img {
    width: 100%;
    position: absolute;
    z-index: -1;
}
```

## Clip path

Images can be visualized in a different shape using the `clip-path` property. Use a generator for this: https://www.cssportal.com/css-clip-path-generator/.

```css
clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
```

## Forms

* Dot not use placeholders only, each input should have a label for accessibility purposes
* Keep forms short
* Form validation should be inline on each element, not at the top of the form

## Radio button checked and unchecked switch style when clicking no JS

```css
input[type="radio"] {
    appearance: none;
    -webkit-appearance: none;
    -moz-appearance: none;
    display: inline-block;
    position: relative;
    border: 2px solid #C6C6C6;
    color: #666;
    top: 10px;
    height: 30px;
    width: 30px;
    border-radius: 50px;
    cursor: pointer;
    margin-right: 7px;
    outline: none;
}

input[type="radio"]:checked::before {
    content: '';
    position: absolute;
    top: 5px;
    left: 5px;
    background: #8040FF;
    width: 16px;
    height: 16px;
    border-radius: 50%;
}
```

