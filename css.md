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
