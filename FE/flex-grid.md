# Flex & Grid

## If the content is shaping the layout, use Flex. If the layout is shaping the content, use Grid

Flex will allow the content to flow and restructure the layout. Grid will instead provide a strict structure to follow.

## Flex

Flex is often used to build individual components, not an entire page layout.

## Parent Properties

`display: flex` places everything in one single row instead of stacking block elements on top of each other.

`flex-direction` sets the direction of the flex. `flex-wrap` is off by default. Set it to `wrap` if there are a lot of items, so they don't overflow.

* With row direction we get columns and work horizontally.
* With column direction we get rows and work vertically.

**`flex-flow: row-reverse wrap` is a shorthand for both.**

`justify-content` deals with how the flex items are distributed along the main axis.

`align-items` deals with how the items are positioned along the cross axis (horizontally on row). It will only work if a container has a height specified.

`align-content` will align content on the cross axix (vertically on row). It's rarely used because it is useful when you have multiple rows of content only.

**The axis will be inverted by changing the direction to column.**

## Child Properties

`flex-grow` and `flex-shrink` will change the speed at which elements grow and shrink inside a container. They are based on a ratio with the default property.

`flex-grow` is set to 0 by default and it does not grow. At 3, it will grow 3 times faster.

`flex-shrink` is set to 1 by default to prevent overflow. At 3, it will shrink 3 times faster.

`flex-basis: 300px` will give a flex child an ideal **width** of 300px at all times. It acts on the main axis, so the value will switch to **height** when `display: flex` is set to column. It is not widely used.

**`flex: 0 1 auto` is the shorthand for grow, shrink and basis. Those are the default values.**

`align-self` will work exactly like `align-items`, but for the child element only.

**When using flexbox, setting the margin top and bottom to auto will center an item vertically in a column layout.**

## Grid

Grid will not let margins collpase either. Once declared, we need to also specify the rows and columns, because unlike Flex, Grid works in both directions.

This line will generate a grid with two rows of 100px, and two columns of 300px.

`grid-template: 100px 100px / 300px 300px`

The below will change the color of the grid items that fit the positioning criteria.

```css
background: green;
grid-row: 2 / 3;
grid-column: 1 / 3;
```

Negative values can be used to make sure something is stretched all the way. Negatives count from the opposite side. Use `grid-colum: 1 / -1`

Spans will make a row or column take up entire grid positions. The column below starts at 2 and spans to 2 positions. The row always spans 2 positions.

```css
grid-column: 2 / span 2;
grid-row: span 2;
```

Grid items stretch by default both horizontally and vertically. If one item is larger, the others will adapt to it.

## Parent Alignment

`justify-items` is looking at the individual cells and will work horizontally on the columns.
`align-items` will do the same vertically on the rows.

## Child Alignment

`justify-self` and `align-self` will do the same, but for the individual cell only.

This image will take up one entire row, all the grid columns, and match it perfectly.

```css
img {
    object-fit: cover;
    grid-row: 1 / 2;
    grid-column: 1 / -1;
    width: 100%;
    height: 100%;
}
```

Instead of using margin, you can simply add an extra row and column with size 1em to have more empty space in a layout.

`grid-gap` will create a gap similar to a padding between the grid items.

When we create a grid, we **explicitly** declare how big the rows and columns are going to be.

If we place an item further down the grid in a position that should not exist, grid will **implicitly** create the cells with size `auto`. Auto defaults to the width and height of the content, but it can be changed with `grid-auto-rows` and `grid-auto-columns`.

`grid-template-areas` has become the standard to name sections in grid. This is much easier for positioning, rather than using the column and row numbers.

## Responsive Grid

`minmax(2em, 5em)` can be used when declaring template sizes to make a layout responsive.

`fr` as a unit will take up a fraction of the space without messing around with other units. It cannot be used as a minimum size in a minmax().

```css
.grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}
```

`repeat()` will help create a grid with similar size elements, for example: `grid-template-columns: repeat(3, 1fr);`

`auto-fit` and `auto-fill` will make a grid responsive and stretch the items. `auto-fit` is more useful because it will stretch what has been declared. `auto-fill` will instead add new, empty columns/rows.

```css
.grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
}
```
