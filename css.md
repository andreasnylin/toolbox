# CSS

## Insert unicode character

```css
/* Inserts a phone followed by a blank space */
.phone:before {
    content: '\260E \0020';
    color: silver;
}
```

## Crossbrowser inline-block

```css
.inline-block() {
	display: inline-block;
	*display: inline;
	*zoom: 1;
}
```

## Clearfix

```css
.clearfix:before, .clearfix:after { 
	content: '';
	display: table;
}

.clearfix:after { 
	clear: both;
}

.clearfix {
	*zoom: 1;
}
```

## Custom color of list bullets/numbers

```css
/* Reset the style of list */
ul, 
ol {
  list-style: none;
  padding: 0;
}

/* Add indentation of nested lists and remove bottom margin */
ul ul,
ol ol {
	padding-left: 1.5em;
	margin: 0;
}

/* Add general display for bullets and numbers */
ul li:before,
ol li:before {
  display: inline-block;
	margin-right: .5em;
  color: red;
}

/* Style for bullet lists */
ul li:before {
	content: '\2022';
	color: red;
}

/* Reset counter for each list */
ol {
	counter-reset: listitem;
}

/* Style for numbered lists. Increment counter for each list item */
ol li:before {
  counter-increment: listitem;
  content: counters(listitem, '.') '.';
}
```

## Box sizing border-box to all elements

```css
/* http://www.paulirish.com/2012/box-sizing-border-box-ftw/ */
/* apply a natural box layout model to all elements, but allowing components to change */
html {
  box-sizing: border-box;
}
*, *:before, *:after {
  box-sizing: inherit;
}
```

## Aspect ratio box

```css
.ar-box {
	position: relative;
	width: 100%;
}

.ar-box:before {
	content: '';
	display: block;
	padding-top: 100%;
}

.ar-box-4-3:before {
    padding-top: 75%;
}

.ar-box-2-1:before {
    padding-top: 50%;
}

.ar-box-1-2:before {
    padding-top: 200%;
}

.ar-box-content {
	position: absolute;
	top: 0;
	left: 0;
	right: 0;
	bottom: 0;
}
```

## Center box

```css
.c-box {
	display: table;
	width: 100%;
	height: 100%;
}

.c-box-content {
	display: table-cell;
	width: 100%;
	height: 100%;
	text-align: center;
	vertical-align: middle;
}
```
