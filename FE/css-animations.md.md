# CSS Animations

## Transitions

Pseudoclasses such as `:hover`  change an element during an action. The transition property allows these changes to occur gradually. `transition: all 0.5s` on an element will ensure that whatever is on its pseudoclass will transition smoothly over half a second. Individual properties instead of `all` can be selected as well, though `delay` is annoying to use. `Transition` is the short-hand for four different properties:

```css
/* shorthand */
transition: font-size 0.5s ease-in 1s;

/* equivalent to below */
transition-property: font-size;
transition-duration: 0.5s;
transition-timing-function: ease-in;
transition-delay: 1s;
```

## Animations

Keyframes are used to create animations by specifying the start and end points. This can be done with `from` and `to`, or with `25% 50% 100%` percentage values of any number.

```css
@keyframes grow {
	from {width: 100px; background: blue}
	to {width: 10px; background: red}
}

@keyframes grow {
	0% {width: 100px; background: blue}
	100% {width: 10px; background: red}
}
```

There are other properties as well that determine other properties in the animation. They all have to go on the element, not the key frame. The shorthand does not take `animation-fill-mode`: it must be placed before the shorthand separately. It is used to determine what happens when an animation ends and it depends in the animation direction as well. Set it to `animation-fill-mode: both` to be safe.

```css
/* not part of the shorthand */
animation-fill-mode: both;

/* shorthand */
animation: grow 1s ease-in 1s 4 alternate;

/* equivalent to below */
animation-name: grow;
animation-duration: 1s;
animation-timing-function: ease-in;
animation-delay: 1s;
animation-iteration-count: 4;
animation-direction: alternate;
```

```css
/* will fade in and expand at the right side */
animation-fill-mode: both;
animation: expand-fade-in 1.5s ease-out;

@keyframes expand-fade-in {
	from {opacity: 0%; width: 0%;}
	to {opacity: 100%; width: 100%;}
}
```

## Transforms

The property `trasform` and its methods are used to change an element in different ways, such as positioning, scaling, rotation, etc. They can be used within keyframes to create cool effects.
* `scale` grows or shrinks an element on the X and Y
* `translate` moves an element on the X and Y
* `rotate` rotates an element clockwise on the X axis by a degree number
* `skew` rotates an element on the X and Y in a 3-d way

```css
/* will scale to x,y = 2,4 */
trasform: scale(2,4)

/* will move to upper left */
transform: translate(-150%, -150%)

/* rotates to the right */
transform: rotate(180deg)

/* turns and flattens */
transform: skew(1360deg, 680deg);

/* combined examples */
@keyframes transform {
	100% {transform: scale(0.5,0.5) rotate(45deg) translate(50px,0px);}
}

@keyframes move {
	to {transform: translate(50vw, 50vh) scaleX(10) skewY(45deg);}
}
```

## Browser compatibility

Prefixes are used to ensure browser compatibility when using transitions, animations and translates.
* `-webkit-` is for mobile browsers
* `-ms-` is for internet explorer
* `-moz-` is for firefox
* `-o-` is for opera

The same property is written again with all the prefixes.

```css
transition: all 0.5s;
-webkit-transition: all 0.5s;
-ms-transition: all 0.5s;
-moz-transition: all 0.5s;
-o-transition: all 0.5s;
```

## Custom variables

Custom variables can be created on the root and then applied with var() anywhere in the stylesheet.

```css
:root {
	--custom-name: 50px;
}

.box {
	width: var(--custom-name);
}
```

## Cubic bezier functions

Cubic bazier functions are used to customize timing on animations: https://cubic-bezier.com.

Two points between 0 and 1 are used to define a curve: the progression on Y, and time on X. It is a timing functions and the curve determines the progression based on time.

They are used on `animation-timing-function` and `transition-timing-function` and implemented already with ease-in, ease-in-out, etc.

