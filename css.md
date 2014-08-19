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
