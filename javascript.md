# JavaScript

## Compare two objects

```javascript
// Simple compare objects in JavaScript. This method works in moste cases
function compareObjs(a, b) {
	var equal = true;
	for(var key in a) {
		if(a.hasOwnProperty(key) && b.hasOwnProperty(key)) {
			if(typeof a[key] === 'function' && typeof b[key] === 'function') {
				continue;
			}
			else if(typeof a[key] === 'object' && typeof b[key] === 'object') {
				if(!compareObjs(a[key], b[key])) {
					equal = false;
					break;
				}
			}
			else if(a[key] !== b[key]) {
				equal = false;
				break;
			}
		}
		else {
			equal = false;
			break;
		}
	}

	return equal;
}

// Usage
var obj1 = { a: 3, b: 'x' };
var obj2 = { a: 3, c: 'y' };
compareObjs(obj1, obj2); // => false

var obj3 = { x: 1, y: 2 };
var obj4 = { x: 1, y: 2 };
compareObjs(obj3, obj4); // => true

var obj5 = { p: { x: 1, y: 1 }, b: 1 }
var obj6 = { p: { x: 1, y: 1 }, b: 1 }

compareObjs(obj5, obj6); // => true
```

## Cookie helper

```javascript
// Inspired by Quirksmode http://www.quirksmode.org/js/cookies.html
var CookieHelper = {
	setCookie: function (name, value, days) {
		days = days || 365;
		var expires = '',
			date = new Date();
	
		date.setTime(date.getTime() + (days * 24 * 60 * 60 * 1000));
		expires = '; expires=' + date.toGMTString();
	
		document.cookie = name + '=' + value + expires + '; path=/';
	},
	
	readCookie: function (name) {
		var nameEQ = name + '=',
			ca = document.cookie.split(';');
		for (var i = 0; i < ca.length; i++) {
			var c = ca[i];
			while (c.charAt(0) == ' ') {
				c = c.substring(1, c.length);
			}
			if (c.indexOf(nameEQ) == 0) {
				return c.substring(nameEQ.length, c.length);
			}
		}
		return null;
	},
	
	deleteCookie: function (name) {
		CookieHelper.setCookie(name,'',-1);
	}
};
```

## Replace all occurrences of a string

```javascript
// Replace all occurrences of monkey
'monkeys monkeys monkeys'.replace(/monkey/g, 'sloth');
// => result: 'sloths sloths sloths'

// Replaces . with ,
'1.5 3.4 6.7'.replace(/\./g, ',');
// => result: '1,5 3,4 6,7'
```

## Split a string on multiple characters

```javascript
// Split a string on multiple characters. This will split on minus, periods and spaces.
'this-is a.string'.split(/[-\.\s]/);
```

## Repeat string

```javascript
Array(5).join('x');
// => result: xxxxx
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

## Create GUID

```javascript
/**
 * Generates a GUID string, according to RFC4122 standards.
 * @returns {String} The generated GUID.
 * @example af8a8416-6e18-a307-bd9c-f2c947bbb3aa
 * @author Slavik Meltser (slavik@meltser.info).
 * @link http://slavik.meltser.info/?p=142
 */
function guid() {
    function _p8(s) {
        var p = (Math.random().toString(16)+"000000000").substr(2,8);
        return s ? "-" + p.substr(0,4) + "-" + p.substr(4,4) : p ;
    }
    return _p8() + _p8(true) + _p8(true) + _p8();
}
```

## Object Store

```javascript
var ObjectStore = {
	values: {},
	length: 0,
	add: function(value) {
		var guid = this.createGuid();
		
		this.values[guid] = value;
		
		this.length++;
		
		return guid;
	},
	remove: function(guid) {
		delete this.values[guid];
		this.length--;
	},
	createGuid: function() {
		function _p8(s) {
			var p = (Math.random().toString(16)+'000000000').substr(2,8);
			return s ? '-' + p.substr(0,4) + '-' + p.substr(4,4) : p ;
		}
		return _p8() + _p8(true) + _p8(true) + _p8();
	}
};
```
