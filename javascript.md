# JavaScript

## Replace all occurrence of a string

```javascript
// Replace all occurrence of monkey
'monkeys monkeys monkeys'.replace(/monkey/g, 'sloth');
// Replaces . with ,
'1.5 3.4 6.7'.replace(/\./g, ',');
```

## Split a string on multiple characters

```javascript
// Split a string on multiple characters. This will split on minus, periods and spaces.
'this-is a.string'.split(/[-\.\s]/);
```

## Generate random number function

```javascript
// Generate random number</span>
function generateRandomNumbers(count, from, to) {
    var nums = [],
        seed = to - from + 1,
            min = from;

    while (count--) {
        nums.push(Math.floor(Math.random() * seed + min))
    }

    return nums;
}

// usage: generateRandomNumbers( how many numbers to generate, from value, to value )
generateRandomNumbers(10, 100, 200);

```

## Array traversing helper methods

```javascript
Array.prototype.skip = function(count) {
	var val,
		length = this.length;

	if(length > count) {
		val = this.slice(count);
	} else {
		val = [];
	}

	return val;
};

Array.prototype.take = function(count) {
	var val,
	length = this.length;

	if(count > length) {
		count = length;
	}

	return this.slice(0, count);
};

Array.prototype.first = function() {
	var val;

	return this.length ? this[0] : this;
};

Array.prototype.last = function(count) {
	var val,
	length = this.length;

	return length ? this[length - 1] : this;
};

var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];

console.log(arr.first());

console.log(arr.last());

console.log(arr.take(3));

console.log(arr.skip(3));
```

## Useful regular expressions

```javascript
// Test a swedish zip code
document.write( /\d{5}|\d{3}\s\d{2}/.test('12345') );
document.write( /\d{5}|\d{3}\s\d{2}/.test('123 45') );
 
// Test email simple
document.write( /^\S+@\S+\.\S+$/.test('zaphod@hotmail.com') );
 
// Test numbers and spaces (phone number)
document.write( /^[0-9\s]+$/.test('070 123 456') );
 
// Replace urls with hyperlinks
var exp = /(\b(?:(?:https?|ftp|file):\/\/|www\.|ftp\.)[-A-Z0-9+&@#/%=~_|$?!:,.]*[A-Z0-9+&@#/%=~_|$])/ig;
var text = 'A url http://www.github.com in a text';
text = text.replace(exp, '<a href="$1" target="_blank">$1</a>');
 
// Remove HTML tags
var regex = /(<([^>]+)>)/ig;
var html = '<p>Test</p>';
document.write(html.replace(regex, ''));
```

## Capitalize first letter in sentance

```javascript
var t='text to capitalize. another sentance.';
t[0].toUpperCase() + t.slice(1).replace(/([.!?]\s*\w)/gi, function(c){ return c.toUpperCase() });
```

## Add remove class from DOM element

```javascript
function addClassToElement(element, className) {
	var classes = element.className.split(' ');
	if(classes.indexOf(className) === -1) {
		classes.push(className);
		element.className = classes.join(' ');
	}
}

function removeClassFromElement(element, className) {
	var classes = element.className.split(' '),
		classNameIndex = classes.indexOf(className);
	
	if(classNameIndex != -1) {
		classes.splice(classNameIndex, 1);
		element.className = classes.join(' ');
	}
}
```

